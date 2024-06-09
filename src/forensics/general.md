# General

1\. Begin with identifying the type of file. At times we may need to know what kind of file we are dealing with. Use the file command to identify your file.

&#x20;                           Syntax:  file \[options] filename

&#x20;                           Options: \`-b\` (brief): Omit the filename in the output.

&#x20;                                            \`-i\` (mime): Output MIME type strings.

&#x20;                                            \`-f\` (files from file): Read filenames from a specified file.

&#x20;                                            \`-L\` (dereference): Follow symbolic links.

&#x20;                                            \`-s\` (special files): Read block or character special files.



2\. Analyzing the file type alone will not give us any leads to go about further.  We can make use&#x20;

of the strings command to print human readable characters hidden within the file(binary   files mostly).&#x20;

Now, why do we use this?&#x20;

The strings command quickly extracts embedded data, flags or sometimes the    indicators of compromise, i.e. URLs/ IP Addresses or file paths to go forward with.&#x20;

&#x20;           Syntax:   strings \[option] file

&#x20;           Options: -a or --all (Scan the entire file, not just the initialized and loaded sections.)

&#x20;                            \-n \<number> (Minimum length of strings to display (default is 4).)

&#x20;                            \-t \<format>( Print the offset before each string. Can be -o, -x or -d)&#x20;

&#x20;                            \-e \<encoding> (Select character encoding)

3\. To get details about the metadata we can use exiftool. It helps understanding the data in hand. Sometimes, we get flags just by using this command.&#x20;

&#x20;            Syntax: exiftool \[OPTIONS] FILE

&#x20;            Options:  -r (Recursively process directories.)

&#x20;                              \-overwrite\_original  (Overwrite original file with edited metadata.)

&#x20;                              \-o ( Write output to specified file.

&#x20;                              \-d (Set date format for output.)

&#x20;                              \-gps:all (Extract all GPS information.)\


4\. Another alternative option to the exiftool to analyze the data is binwalk.&#x20;

It can extract data embedded within files like firmware images, executable and disc images.&#x20;

&#x20;               Syntax:  binwalk \[OPTIONS] FILE(S)

&#x20;               Installation: sudo apt-get install binwalk

&#x20;               Options: -B (Only scan for file signatures.)

&#x20;                                \-e ( Automatically extract files from input.)

&#x20;                                \-M or -matryoshka (Recursively scan extracted files.)

&#x20;                                \-y  (Search for known executable code within files.)

&#x20;                                \-l  (List all available extraction signatures.)

&#x20;                                \-D ( Disassemble extracted code.)

#### WALKTHROUGH 1

We shall see an easy example

Information(picoCTF): [https://play.picoctf.org/practice/challenge/186?category=4\&page=1](https://play.picoctf.org/practice/challenge/186?category=4\&page=1)

Let us start with identifying the file using the file command. This gives us the file details such as its a jpg image file. We shall continue executing commands as in our general list. You should be looking for any suspicious looking strings. Now on executing exiftool we observe something uncanny.&#x20;

\
![](https://lh7-us.googleusercontent.com/docsz/AD\_4nXfYRVrlCV6DbUNrauFzCHVa-1n7ypEfhXAAu4lFVDiNZ6RcbgL5nGRiopC2LxHQALEz3n7HrSNPfBfxi894zl0sWTjOGty45ZdAWov6VCk0\_zZfPAZcJ7GjULDXX7H2sILz-dXHmn09PW7WKS8TQTQjbzg?key=3tC4LW6BC-ghAujvhgrQ3Q)

We can see that the License here consists of both uppercase and lower case characters. This could be encoded in Base64.  Now, what is Base64? It is a binary text encoded using ASCII strings. It usually has an = at the end of it (not in this case, its just a padding character.), that is one way you can identify that it is base64.&#x20;

Now just copy the License: cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9

And paste it onto any Base64 decoder available online.&#x20;

You should get your flag: picoCTF{the\_m3tadata\_1s\_modified}
