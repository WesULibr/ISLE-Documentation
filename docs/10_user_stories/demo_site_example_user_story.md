<!--- PAGE_TITLE --->

## Testing ISLE

Alice is curious about ISLE and wants to know more about using Islandora for her university's digital collections.  She does not have access to a server and would like to test drive Islandora before deciding whether or not to move forward with it.

Alice has a Windows 10 laptop and she has confirmed that it meets the [Hardware Requirements](../01_installation_host_server/hardware-requirements.md) for testing ISLE.  She also has Administrator rights on her laptop.

She begins by installing Docker for Windows and configuring her system so ISLE can run on it by following the [Software Dependencies](../01_installation_host_server/software-dependencies.md) instructions.  Next, Alice starts the services that make up ISLE and installs Islandora on a virtual machine running on her laptop using the [Demo ISLE Site Installation Guide](../02_installation_demo_site/demo_installation.md).  Because this is a test site that can only be viewed on Alice's laptop, she does not need to make many config file changes and is safe using default settings.

Alice now has a working version of ISLE running on her laptop!  She can ingest new objects, view and edit exising objects, and safely test new settings.  When she is done testing, she can easily shut down ISLE with a single command, then start it again just as easily at another time to continue testing or demo it to colleagues.  If she decides to wipe out all of the changes she has made and start over with a fresh installation, she just has to delete the ISLE directory on her laptop and download the ISLE containers again--a process that usually takes no more than several minutes.