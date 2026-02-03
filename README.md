declare
	r boolean;
	cnt number;
begin
	If :t_fur_mstr.NVL_FUR_NAME='A' or :t_fur_mstr.NVL_FUR_NAME='B' or :t_fur_mstr.NVL_FUR_NAME='C' Then
		select count(lot_no) into cnt from t_tap_hole_clay where supplier=:t_cast_details.mg_clay_used and fur_name in ('A','B','C')  and bag_in_stock>0;
  	If cnt>0 Then
			r:=show_lov('lov_lotnoabc');
  	Else
  		Message('No Lot No. Exists Against The Selected Clay Type !!');
  		Message('No Lot No. Exists Against The Selected Clay Type !!');
  	End If;	
	Else
		select count(lot_no) into cnt from t_tap_hole_clay where supplier=:t_cast_details.mg_clay_used and fur_name=:t_fur_mstr.NVL_FUR_NAME  and bag_in_stock>0;
  	If cnt>0 Then
			r:=show_lov('lov_lotno');
  	Else
  		Message('No Lot No. Exists Against The Selected Clay Type !!');
  		Message('No Lot No. Exists Against The Selected Clay Type !!');
  	End If;
	End If;
	
Exception 
  When Others Then Null;
	
end;
