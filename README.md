IF :TIMESTAMP.NVL_DATE IS NOT NULL  AND :TIMESTAMP.NVL_SHIFT IS NOT NULL THEN
				
				SELECT COUNT(*) INTO VCOUNT 
				FROM DEMO.T_BF_SIGNOFF 
				WHERE SO_DATE  = :TIMESTAMP.NVL_DATE  AND 
				      SO_SHIFT = :TIMESTAMP.NVL_SHIFT AND 
				      SO_PAGE  = 'COKE_UNLOADING';
				
				IF VCOUNT >0 THEN
						UPDATE DEMO.T_BF_SIGNOFF 
						SET SO_CHECK    = :T_BF_SIGNOFF_UNLOADING.SO_CHECK,
								NAME        = :T_BF_SIGNOFF_UNLOADING.NAME,
								SO_TIME     = SYSDATE
						WHERE SO_DATE    = :TIMESTAMP.NVL_DATE  AND 
						      SO_SHIFT   = :TIMESTAMP.NVL_SHIFT AND 
						      SO_PAGE    = 'COKE_UNLOADING';
				ELSE
								insert into DEMO.T_BF_SIGNOFF
								      (NAME,
								       SO_DATE,
								       SO_SHIFT,
								       SO_CHECK,
								       SO_TIME,
								       SO_PAGE)
							  values(:T_BF_SIGNOFF_UNLOADING.NAME,
							         :TIMESTAMP.NVL_DATE,
							         :TIMESTAMP.NVL_SHIFT,
							         :T_BF_SIGNOFF_UNLOADING.SO_CHECK,
							         SYSDATE,
							         'COKE_UNLOADING');
				END IF;
				
					COMMIT;		
					IF :T_BF_SIGNOFF_UNLOADING.SO_CHECK = 1 THEN	
             set_item_property('TIMESTAMP.PBSAVE',enabled,property_false);
					   set_item_property('TIMESTAMP.PBDELETE',enabled,property_false);
					ELSE
 					   set_item_property('TIMESTAMP.PBSAVE',enabled,property_TRUE);
					   set_item_property('TIMESTAMP.PBDELETE',enabled,property_TRUE);
					END IF;
			END IF;
