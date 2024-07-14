# AveMe
simple CHAT
<!DOCTYPE html>
<html lang="ru">  

<head>  
<title>ЧАТ</title> 
<meta charset="UTF-8"> 
</head>

<body>
 
<form method="POST" id="form">  
  <textarea id="txarea"  wrap="hard" name="message"  autofocus  placeholder="введите текст" required autocomplete="off"></textarea> 
    <button onclick="myFunction()" type="submit" name="enter" value="кнопка" title="отправить текст">
	</button>

<script>
let timeout;
function myFunction() {
timeout = setTimeout(clFunc, 150);}
function clFunc() {
let textarea = document.querySelector('#txarea');
textarea.value = '';
}
</script>

<div id="slider">	  
	<script type="text/javascript">
            setInterval(function(){
            $('#slider').load('chatD.php');
            }, 100) 
    </script>
</div>

<script>
  document.getElementById('form').onsubmit = async function(e) {
    e.preventDefault();
    const formData = new FormData(this);
    const response = await fetch('write.php', {
      method: "POST",
      body: formData,
    });
    const text = await response.text();
    document.getElementById('slider').innerHTML = text;
  }
</script>

</body>
</html>


<!-- file chatD.php -->
<?php
/**/
if(isset($_POST["enter"]))
{	
$filename = "text.txt";
$textMessage = htmlspecialchars($filename);
$file = fopen($textMessage, "a");
fwrite($file, $_POST['message']."\n");}
$file = fopen("text.txt","r");
while(! feof($file)) {
  $line = fgets($file);
  echo $line."<br>";
}
fclose($file); ?>


<!-- file write.php -->
<?php
if($_POST) {
  $filename = 'text.txt';
  $textMessage = htmlspecialchars($filename);
  file_put_contents($textMessage, $_POST['message'].PHP_EOL, FILE_APPEND);
  $out = file_get_contents($filename);
  echo nl2br($out);
}
?>
