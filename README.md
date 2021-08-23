
<html>
<head>

</head>
<body>

<h1>Remove plagirism from text</h1>
<p>Enter text to remove plag.</p>
  
  <textarea id="message" rows="20" cols="50"></textarea>
  <br><br>
   <input type="button" value="Get Text" onclick="getText()" />

  <script>
  function getText() {
    var text = document.getElementById("message").value;
    alert(text);
}
  </script>
  


</body>
</html>
