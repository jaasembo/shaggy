<?php
//my proudest code thus far
require_once "../moss/app_config.php";
require_once "../moss/Database_Connect.php";
$upload_dir = HOST_WWW_ROOT . "uploads/car_pics/";
//for the thumnails
$upload_dir1 = HOST_WWW_ROOT . "uploads/FrontSide_Right/";
$upload_dir2 = HOST_WWW_ROOT . "uploads/FrontSide_Left/";
$upload_dir3 = HOST_WWW_ROOT . "uploads/BackSide_Right/";
$upload_dir4 = HOST_WWW_ROOT . "uploads/BackSide_Left/";
$upload_dir5 = HOST_WWW_ROOT . "uploads/Engine/";
$image_fieldname = "file_name";
$image_thumb1 = "FrontSide_Right";
$image_thumb2="FrontSide_Left";
$image_thumb3="BackSide_Right";
$image_thumb4="BackSide_Left";
$image_thumb5="Engine";
//this code use two tables to store different objects 
//It starts by loading images into a file system and then pushing them to tables
$php_errors = array(1=>'Maximum file size in php.ini exceeded',
                    2=>'Maximum file size in HTML form exceeded',
					3=>'Only part of the file was uploaded',
					4=>'No file was selected to upload.');
$VIN=trim($_REQUEST['VIN']);
$YEAR=trim($_REQUEST['YEAR']);
$MAKE=trim($_REQUEST['Make']);
$MODEL=trim($_REQUEST['Model']);
$PRICE=trim($_REQUEST['Asking_Price']);
$COLOR=trim($_REQUEST['EXT_COLOR']);
$PPRICE=trim($_REQUEST['PURCHASE_PRICE']);
$MILEAGE=trim($_REQUEST['MILEAGE']);
$TRANSMISSION=trim($_REQUEST['TRANSMISSION']);
$DPRICE=trim($_REQUEST['PURCHASE_DATE']);
$SPRICE=trim($_REQUEST['SALES_DATE']);
$SHIP=trim($_REQUEST['SHIP_DATE']);
$ICOLOR=trim($_REQUEST['INTERIOR_COLOR']);
//NUMBER 1
($_FILES[$image_thumb1]['error'] ==0)
 or handle_error("the server couldn't upload the image you selected.",
                 $php_errors[$_FILES[$image_thumb1]['error']]);
		   
$now= time();
 while(file_exists($upload_filename1 = $upload_dir1 . $now .
                                    '_' .
                                    $_FILES[$image_thumb1]['name'])){
  $now++;									
}	
@move_uploaded_file($_FILES[$image_thumb1]['tmp_name'],$upload_filename1)
 or handle_error("We had a problem saving your image to" .
 "its permanent location.",
 "permissions or related error moving " .
 "file to{$upload_filename1}");

//NUMBER 2
($_FILES[$image_thumb2]['error'] ==0)
 or handle_error("the server couldn't upload the image you selected.",
                 $php_errors[$_FILES[$image_thumb2]['error']]);
		   
$now= time();
 while(file_exists($upload_filename2 = $upload_dir2 . $now .
                                    '_' .
                                    $_FILES[$image_thumb2]['name'])){
  $now++;									
}	
@move_uploaded_file($_FILES[$image_thumb2]['tmp_name'],$upload_filename2)
 or handle_error("We had a problem saving your image to" .
 "its permanent location.",
 "permissions or related error moving " .
 "file to{$upload_filename2}");		
//NUMBER 3
($_FILES[$image_thumb3]['error'] ==0)
 or handle_error("the server couldn't upload the image you selected.",
                 $php_errors[$_FILES[$image_thumb3]['error']]);
		   
$now= time();
 while(file_exists($upload_filename3 = $upload_dir3 . $now .
                                    '_' .
                                    $_FILES[$image_thumb3]['name'])){
  $now++;									
}	
@move_uploaded_file($_FILES[$image_thumb3]['tmp_name'],$upload_filename3)
 or handle_error("We had a problem saving your image to" .
 "its permanent location.",
 "permissions or related error moving " .
 "file to{$upload_filename3}");		
//NUMBER 4
($_FILES[$image_thumb4]['error'] ==0)
 or handle_error("the server couldn't upload the image you selected.",
                 $php_errors[$_FILES[$image_thumb4]['error']]);
		   
$now= time();
 while(file_exists($upload_filename4 = $upload_dir4 . $now .
                                    '_' .
                                    $_FILES[$image_thumb4]['name'])){
  $now++;									
}	
@move_uploaded_file($_FILES[$image_thumb4]['tmp_name'],$upload_filename4)
 or handle_error("We had a problem saving your image to" .
 "its permanent location.",
 "permissions or related error moving " .
 "file to{$upload_filename4}");		
//NUMBER 5
($_FILES[$image_thumb5]['error'] ==0)
 or handle_error("the server couldn't upload the image you selected.",
                 $php_errors[$_FILES[$image_thumb5]['error']]);
		   
$now= time();
 while(file_exists($upload_filename5 = $upload_dir5 . $now .
                                    '_' .
                                    $_FILES[$image_thumb5]['name'])){
  $now++;									
}	
@move_uploaded_file($_FILES[$image_thumb5]['tmp_name'],$upload_filename5)
 or handle_error("We had a problem saving your image to" .
 "its permanent location.",
 "permissions or related error moving " .
 "file to{$upload_filename5}");	
$query=sprintf("INSERT INTO images " . 
"(FrontSide_Right,FrontSide_Left,BackSide_Right,BackSide_Left,Engine)" .
"VALUES('%s','%s','%s','%s','%s');",
mysql_real_escape_string($upload_filename1),
mysql_real_escape_string($upload_filename2),
mysql_real_escape_string($upload_filename3),
mysql_real_escape_string($upload_filename4),
mysql_real_escape_string($upload_filename5),
mysql_insert_id());
mysql_query($query)
or die(mysql_error());
	
($_FILES[$image_fieldname]['error'] ==0)
 or handle_error("the server couldn't upload the image you selected.",
                 $php_errors[$_FILES[$image_fieldname]['error']]);
		   
$now= time();
 while(file_exists($upload_filename = $upload_dir . $now .
                                    '_' .
                                    $_FILES[$image_fieldname]['name'])){
  $now++;									
}	
@move_uploaded_file($_FILES[$image_fieldname]['tmp_name'],$upload_filename)
 or handle_error("We had a problem saving your image to" .
 "its permanent location.",
 "permissions or related error moving " .
 "file to{$upload_filename}");									
$query=sprintf("INSERT INTO cars " .
"(VIN,Make,Model,ASKING_PRICE,EXT_COLOR,PURCHASE_PRICE,MILEAGE,TRANSMISSION,PURCHASE_DATE,SALES_DATE,SHIP_DATE,INTERIOR_COLOR,user_pic_path,image_path_id)" .
"VALUES(%d,'%s','%s',%d,'%s',%d,%d,'%s',%d,%d,%d,'%s','%s','%d');",
mysql_real_escape_string($VIN),
mysql_real_escape_string($MAKE),
mysql_real_escape_string($MODEL),
mysql_real_escape_string($PRICE),
mysql_real_escape_string($COLOR),
mysql_real_escape_string($PPRICE),
mysql_real_escape_string($MILEAGE),
mysql_real_escape_string($TRANSMISSION),
mysql_real_escape_string($DPRICE),
mysql_real_escape_string($SPRICE),
mysql_real_escape_string($SHIP),
mysql_real_escape_string($ICOLOR),
mysql_real_escape_string($upload_filename),
mysql_insert_id());
mysql_query($query)
or die(mysql_error());



?>
<?php header("Location: Show_Inventory.php");?>
