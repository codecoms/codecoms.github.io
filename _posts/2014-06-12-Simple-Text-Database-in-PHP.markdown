---
layout: post
title:  "Simple Text File Database in PHP"
subtitle: "Create and maintain a sequential text database in PHP"
date:   2014-06-12 16:20:40
tags:
  - PHP
  - Text database
  - Code
  - PHP programming
categories: PHP
tags: [php, programming, code, text database]
---
Sometimes you need to capture data sequentially without structured tables or relationships. In this case a SQL database is overkill and unnecessarily complex for the task at hand.  

To see the demo click [here].

This project has two components: a text file we use as database and a HTML/PHP page.
For simplicity I separated the files into HTML and PHP.

* Text file: *data.txt*
* HTML: *index.html*
* PHP engine: *databaseAction.php*

**Note:** *the HTML and PHP file can be combined in one single PHP file that calls itself with the use of the `$_SERVER['PHP_SELF']` variable (this is what I did in the live demo).*

###How it works
The  HTML page calls the PHP script to manipulate the text database. Simple and effective.

The actions we can perform on the database are the following:

1. Add a new record (sequentially)
2. Empty the database
3. Display all the records in the database (all the lines in the text file) with the option to delete a selected line
4. Be able to backup the database when needed (not present in the live demo)

The record added will be in the form of *timestamp,note*, for example: 

`Wednesday Jun 11 2014 20:54:54,first record`<br>
`Thursday Jun 12 2014 22:07:55,second record`<br>
`Thursday Jun 12 2014 21:08:14,third record`<br>

The HTML source code:

{% highlight html %}

	<head>
		<meta charset="utf-8" />
	    <title>Text File Database Demo</title>
	</head>
	<body>
	
	<form action="databaseAction.php" method="post">
	
	Add a Record: <button type="submit"> Timestamp </button>
	Notes: <input type="text" name="note">
	<input type=hidden name=operation value=1>
	<p></p>
	</form>
	
	<form action="databaseAction.php" method="post">
	<input type=hidden name=operation value=2>
	Clear Data: <button type="submit">Erase</button>
	<p></p>
	</form>
	
	<form action="databaseAction.php" method="post">
	<input type=hidden name=operation value=3>
	Records in the Database: <button type="submit">Show</button>
	<p></p>
	</form>
	
	<form action="databaseAction.php"
      method="post">
      <input type=hidden name=operation value=5>
      <p>Backup the database: <button type="submit">Backup</button>
      </p>
    </form>

{% endhighlight %}

The PHP file that performs the selected actions to the file is quite simple. I use the `Switch/Case` control structure to select what operation to perform.

* The fopen function allows you to read/write/append to a text file through a file handler  variable (in our case the variable $f


 
* I use the `ftruncate` function to clear the file. This function truncates a file to a given length (in this case 0
)
* Very interesting is the `cutline` function on line 57. What that 
function does is delete the line in the file with a specific number. 
I found the function on some PHP help website I shamelessly copied it. It works great (first rule of programming: never reinvent the wheel, use what’s out there).

* To display the records I use the PHP function `explode` to split the record at the comma and show the timestamp and the note separately for an easier read

{% highlight php %}

<?php

if (!isset($operation)) {
	$operation = 0;
}


$id=$_REQUEST['operation'];
$note =$_REQUEST['note'];


if (empty($note)) {
	$note = 'N/A';
}

$dataFile = "data.txt";
$time = date("l M d Y H:i:s", strtotime('+2 hours'));

$record = $time.",".$note.PHP_EOL;

switch($id) {

    case 1: //insert new recordi

	$fh = fopen($dataFile, 'a') or die("can't open file");
	fwrite($fh, $record);
	fclose($fh);

	print "<p>Inserted: ".$record."</p>";
	print '<p> <a href=data.txt>Data File</a> </p>';

    break;

    case 2: //clear file
	$fh = fopen( $dataFile, "r+" );
	ftruncate($fh, 0);
	fclose($fh);

	print "<p> Content Erased! <a href=$dataFile>Check here</a> </p>";


    break;

    case 3; //list the content of the file
	$count = substr_count(file_get_contents($dataFile), "\n");
	print "<p>".$count." record(s) in the text database: <br>";

	$fh = fopen($dataFile, 'r') or die("can't open file");
	$n = 1;

	for ($i=1; $i<$count+1; $i++){
		$line = fgets($fh, 1024);
		$list = explode(",", $line);
		$r = urlencode($line);
		print $i.") ".$list[0]." => ".$list[1]." | "."<a href=$self?operation=4&line_no=\"$i\" onclick=\"return confirm('Delete the record?')\">delete</a>"."<br>";
	}
	print "</p>";
	fclose($fh);

    break;

    case 4; //delete line
	function cutline($filename,$line_no=-1) {

		$strip_return=FALSE;

		$data=file($filename);
		$pipe=fopen($filename,'w');
		$size=count($data);

		if($line_no==-1) $skip=$size-1;
		else $skip=$line_no-1;

		for($line=0;$line<$size;$line++)
		if($line!=$skip)
		fputs($pipe,$data[$line]);
		else
		$strip_return=TRUE;
		return $strip_return;
	}

	$line_no = trim ( $_GET['line_no'], '"') ;

	cutline($dataFile, $line_no); // deletes line
    break;


    case 5: //Backup the file

	$d = new DateTime();
	$timeStamp = $d -> getTimestamp();

	$backupFile = "backup/dataBackup_$timeStamp.txt";

	if (!copy($dataFile, $backupFile)) {
		print  "<p>Failed to backup the database! $dataFile, $backupFile</p>";
	} else {
		print "<p> Backup succeded!<br> "."<a href=\"$backupFile\">Examine the backed up file</a></p>";
	}

    break;

    case 99;
	show_source(__FILE__);

    break;

    case 0: //do nothing

    break;

}

?>

{% endhighlight %}

<p>&nbsp;</p>
{% include twitter_plug.html %}







[here]: http://www.paini.org/federico/TextDatabase/index.php