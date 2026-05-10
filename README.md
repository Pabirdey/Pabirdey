 SELECT COUNT(*) INTO VCOUNT 
     FROM DEMO.T_BF_SIGNOFF 
     WHERE SO_DATE     = :TIMESTAMP.NVL_DATE  AND 
           SO_SHIFT    = :TIMESTAMP.NVL_SHIFT AND 
           SO_PAGE     = 'COKE_UNLOADING' and 
           SO_CHECK    = 1;
		 if VCOUNT>0 then
  		 set_item_property('TIMESTAMP.PBSAVE',enabled,property_false);
		   set_item_property('TIMESTAMP.PBDELETE',enabled,property_false);
		  					 
  		 select NAME,SO_CHECK into :T_BF_SIGNOFF_UNLOADING.NAME,:T_BF_SIGNOFF_UNLOADING.SO_CHECK   
  		 FROM DEMO.T_BF_SIGNOFF 
  		 WHERE SO_DATE    = :TIMESTAMP.NVL_DATE  AND 
  		       SO_SHIFT   = :TIMESTAMP.NVL_SHIFT AND 
  		       SO_PAGE    = 'COKE_UNLOADING';
							 
		 else
		   go_block('T_BF_SIGNOFF_UNLOADING');
	  	 clear_block;
	  	 set_item_property('TIMESTAMP.PBSAVE',enabled,property_true);
		   set_item_property('TIMESTAMP.PBDELETE',enabled,property_true);
		 end if;

If (:TIMESTAMP.NVL_DATE is not null) and (:TIMESTAMP.NVL_SHIFT is not null )	 Then
		 PROC_POPULATE_COKEUNLOADING(:TIMESTAMP.NVL_DATE,:TIMESTAMP.NVL_SHIFT);
		 PROC_POPULATE_HIGHLINE_DATA(:TIMESTAMP.NVL_DATE,:TIMESTAMP.NVL_SHIFT);
		 PROC_POPULATE_RAWMATERIAL_POSI(:TIMESTAMP.NVL_DATE,:TIMESTAMP.NVL_SHIFT);
		 PROC_POPULATE_UNLOAD_REP(:TIMESTAMP.NVL_DATE,:TIMESTAMP.NVL_SHIFT);
		 --null;
End If;
