# Installing Subclipse in Eclipse/PDT or Zend Studio

## Big Assumption
It may be possible to have both Subclipse and Subversive installed at the same time. I have not 
tested it and am not sure how it would work. These instructions assume that you are abandoning 
your previous Subversive checkouts of your projects and re-importing them using Subclipse. Let 
me know if you experiment with another method that works.

## Overview
Using Subclipse requires the Collabnet Subversion distribution. These binary packages are created 
by the company that sponsors Subversion and are always kept at bleeding edge versions. They are 
required because they also include the native Java bindings that Subclipse requires. The advantage 
of this is that you can also use the CLI Subversion client or any other desktop SVN client that 
supports Subversion 1.6.

## Installing the Collabnet Subversion distribution
1. Download the proper package here: http://www.open.collab.net/downloads/community/
2. Install the subversion package
3. Modify your bash path to prefer the new SVN binaries over the OS X ones.
4. Restart your shell and test that you are using the correct SVN by running "which svn" 
	The output should be "/opt/subversion/bin/svn"

## Installing Subclipse
1. Uninstall Subversive via the "Installation details" dialog. You can get to this via the "About" 
	dialog or the "Install new software…" dialog.
2. Delete your previous projects in your workspace (or just create a new workspace). Make sure you 
	also delete the contents on the disk. Your workspace folder should be except for the ".metadata" 
	folder.
3. Restart Eclipse
4. Open the "Install new software…" dialog.
5. Click "Add…" to add a new update site. Add http://subclipse.tigris.org/update_1.6.x
6. Select this new update site in the UI and install all Subclipse components
7. Restart Eclipse again and you should be up and running with Subclipse as the new SVN Team 
	provider. You can use "Import..." as usual to create your projects again.