A multithreaded web server with a frontend and processing modules
![[Pasted image 20240530083601.png]]
Processing module involves various steps:
- Resolve name of Webpage requested
- Perform access control on webpage
- Check in cache
- Fetch Requested page from disk or run program
- Determine rest of response
- Return response to client
- Make entry in server log

**Example of web cache:**
![[Pasted image 20240530084057.png]]
Cookies often used for tracking on server side