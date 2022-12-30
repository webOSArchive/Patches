# Creating Patches

This project includes tools and notes for generating patches for legacy (mobile) webOS

## .patch Files (Unpackaged)

Use **UnifiedDiffCreator.jar**:

- Find file location on device
- Copy file off device
- Duplicate file and edit copy
- Run Unified Diff Creator, giving original file, edited duplicate, and original location on device
- Press 'Create Patch'

Resulting `.patch` file can be run by WOSQI as-is, but can't be run in Preware for some reason

## .ipk Files (Packaged)

### Without a .patch
See the `source/script-only` folder for starter structure

- Use an empty `data` folder
- Modify the `control` file with your metadata
- Modify the `postinst` script to do whatever you want on install
- Modify the `prerm` script to do whatever you want on remove

Use **IpkPackager.jar**:

- See IpkPackager notes below...
- Select your `data` folder from its parent
- Specify your scripts
- Press 'Create IPK File'

Resulting `.ipk` file can be run via WOSQI or Preware

### With a .patch
Generate your `.patch` file first (see above)
See the `source/scripted-patch` folder for starter structure

- Same as above, but include your `.patch` in the `data` folder

## IpkPackager Notes

- **Folder**: click folder from *parent* of folder with *actual .patch file* in it
- **Destination on device**: */media/cryptofs/apps*`/usr/palm/applications/org.webosarchive.patches.patch-name`
- **Name:** Human readable
- **ID:** same as Folder name (org.webosarchive.etc)
- **Version:** 1.0.0
- **Developer:** Human name
- **Depends:** 
	- `org.webosinternals.patch`
	- `org.webosinternals.lsdiff`
- **Postinst script:** find `postinst` script from patch project
- **Prerm script:** find `prerm` script from patch project

## Install Process Notes

- `control` files deployed to: `/media/cryptofs/apps/usr/lib/ipkg/info`
- `data` files deployed to: `/media/cryptofs/apps/usr/palm/applications`
- `postinst` file is executed, errors shown in WOSQI/Preware come from this script