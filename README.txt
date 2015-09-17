htmlMimeMail3 is a drop in replacement for the original htmlMimeMail.

NOTE TO USERS:
Because this project serves primarily for our production purposes, I make no
guarantees that the API will not change. If it does change, all changes will
be noted in the changelog.txt and the API.txt documents. The most likely to
be changed are the attachment and image add items.

The project has been forked, and updated to work without errors on current PHP
versions. Tested and debugged on:

PHP Version 5.6.12-1 (development, full error reporting on, warnings, etc)
PHP Version 5.3.29 

IMPORTANT: this version is not fully compatible with version 5 of htmlMimeMail.
See the htmlMimeMail5 documentation page for a list of the differences. 

http://www.homer.com.au/webdoc/htmlMimeMail/htmlMimeMail5.htm

I may end up adding the changed 5 syntax to 3.0, but for now, the 
image/attachment syntax follows 2.5.

This is version 5 syntax:
$mail->addEmbeddedImage(new fileEmbeddedImage('background.gif', 
'image/gif', new Base64Encoding()));

$mail->addAttachment(new fileAttachment('example.zip', 
'application/zip', new Base64Encoding()));

See API.txt for the 2.5/3.0 syntax.

WHY FORK htmlMimeMail 2.5 AND NOT 5.0?
Because htmlMimeMail5 contained some updates and improvements that were actually
undesirable for our application, I decided to fork the 2.5 version from 2002, 
which we have been running since about 2003 without any problems, and which
meets our use case perfectly.

The smtp.php and RFC822.php libraries were taken from the 5.0 release and then
updated, since nothing in them particularly conflicted with our needs.

Note that nothing changes at all if you were using htmlMimeMail 2.5 from 2002,
and only a few small things change if you are using 5.0.

Because I've always really liked this class, and found it to be neat, tightly
written, and overall perfect for our needs in production, I decided that it is
best to fork it, and then maintain the updated version, which we run live in
fairly heavy production use.

The 3.0 release is intended for our purposes primarily, and with that in mind,
we have no interest in anything but making sure the code is solid, clean, and
bug free.

The main reason I didn't use htmlMimeMail5 was that it splits all emails into
text AND / OR html, using email boundaries, which creates a situation that is
actually a negative for our needs. htmlMimeMail5 is also more complicated, and
doesn't really do anything that we need. I may now and then pull pieces off of
it and put them into 3.0 if they prove to be more reliable and do not change
the functionality of the 3.0 release at all. As noted, smpt.php and RFC822.php
are from the 5.0 release.

Please do not ask for support, I included the original example files from the
original download release, and the API.txt, my purpose in releasing this is
purely to help maintain what I have always felt to be a very fine class that
did its job in clean Unix way, ie, do one thing, and do it well.

There are bigger classes out there, more complicated, probably orders of 
magnititude larger, if you want one of those, I urge you to use them. This
is a simple clean class, that does what it is supposed to do.

BUGS FIXED:
There were a few bugs in the original and version 5.0 that have not been 
corrected. Version 3.0 corrects the following bugs:
------------------------------------
1:
http://www.phpclasses.org/discuss/package/32/thread/4/
The _encode_header() functionremoves wanted whitespace when there are 
Umlauts (����) in the subject line. 
------------------------------------
2:
I fixed another one, where the RFC spec was incorrectly implemented:
http://www.w3.org/Protocols/rfc822/3_Lexical.html
_validateAtom()

returned false for valid email: jones.fred <jones.fred@fred.com>
because it was searching for a dot as an invalid character.

DEVELOPERS:
Please note: I have cleaned up the indentation, and the code, so if you want
to contribute, please make sure to use the proper indentation (TABS), and
do NOT use oneliner flow controls, or skip brackets, etc. There's no reason
to do that, and all those practices do is hide bugs and issues, and make the
code hard to read, for no gain at all.
Example:
BAD: 
if ($m) execute_code();

GOOD: 
if ( $m ) {
	execute_code();
}

Pull requests are welcome as long as they improve the overall code quality,
get rid of deprecated features, and prepare the class for any future PHP 
updates.

Pull requests that try to add undesirable features, or features that break our
core requirements, will of course not be accepted.

All patches should be tested in real production situations, not just local
servers.

Note: I was never any good at the old PHP class programming, so some of the
code in this class is a bit of a mystery to me. Nor am I particularly good at
current PHP class syntax and best practices, so if you spot something that
seems wrong and which should be cleaned up, by all means, let me know, submit
a patch, a pull request, etc, but always remember, the existing functionality
can never be changed without prior discussion and approval because this is
used commercially in a live setting.