# deleteex #

There was an interesting discussion on NTFSD recently due to a file that could not be deleted:


    http://www.osronline.com/showThread.CFM?link=286551
 
The issue was due to the fact that the file had an active image section (i.e. was currently loaded as an executable). However, the poster was only trying to delete **a** hard link to the file, not the **last** hard link to the file.

In playing with this more, it turns out that this case is properly handled by NTFS if you send the new FileDispositionInfoEx request. This will allow the link to be deleted even though there is an active image section, so long as it's not the last link to the file. This test application demonstrates the new behavior.

# Building the sample #
The provided solution builds using Visual Studio 2017. The target system must be running Windows 10 RS3 or later in order for the test to succeed.





