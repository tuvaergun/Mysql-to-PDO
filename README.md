Mysql-to-PDO
============

<?php
//mysql sunucuya  bağlanma ve veritabanı seçme
  //mysql
  mysql_connect('localhost','root','parola');
  mysql_select_db('deneme');
  //pdo
  $db = new PDO('mysql:host=localhost;dbname=deneme','root',parola);
 
//sorgu
  $sqlUyeler = 'select * from uyeler where cins="2"';
  
  //mysql
  $qryUyeler = mysql_query($sqlUyeler);
  
  //pdo 
  $qryUyeler = $db->exec($sqlUyeler);
  
  //Döngü :
 
  
  //mysql 
  while($rslUyeler = mysql_fetch_assoc($qryUyeler))
  {
    echo '<pre>';
    print_r($rslUyeler);
    echo '</pre>';
  }
  
  //pdo 
   while($rslUyeler = $qryUyeler->fetch(PDO:FETCH_ASSOC))
  {
    echo '<pre>';
    print_r($rslUyeler);
    echo '</pre>';
  }
  
  
  //mysql_quey yerine $db->exec kullanabilirsiniz
  mysql_query('Delete From Uyeler where id=1');
  $db->exec('Delete From Uyeler where id=1');
  
  /*
    PDO avantajı : özellikle sql injection zaafiyetinden korunmak için parametreli sorgu diye 
    özetleyebilecğeimiz bir yapı kullanabilirsiniz.
  
  */
  $cins = 1;
  $il = 34;
  $sonuc=$db->prepare("SELECT * FROM uyeler WHERE cins=? and il=?");
  $sonuc->execute(array($cins,$il));
  while($uye = $sonuc->fetch(PDO:FETCH_ASSOC))
  {
     echo '<pre>';
    print_r($uye);
    echo '</pre>';
    
  }
  
