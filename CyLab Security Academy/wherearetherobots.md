# where are the robots challenge

Objective: Can you find the Robots?

How-to-Solve:
1. Click the 'Launch instance' button. The new instance will be create and new link like this ( http://chatelaine.cylabacademy.net:40392 ) will appear then click the link. (Please note that the urls may vary for each user, depending on how CyLab generates the URL.) 
2. After clicking the link, we will be directed to a website like this screenshot <img width="1917" height="972" alt="Screenshot 2026-10-03 080545" src="https://github.com/user-attachments/assets/8a37403c-e9a1-4b6d-a44b-6d92bbb78854" /> .
3. To find where the robots file is, we need to add path/file '/robots.txt' at the end of the urls address. So the urls will look like this (http://chatelaine.cylabacademy.net:40392/robots.txt) and click enter.
4. After click the enter button, the website will redirect into file robots.txt where the file contain two information: User-agent: * and Disallow: /47a0d.html . We can use this two information to find the flag. In the Disallow information, there is a file called '/47a0d.html'. So we can add it into the urls like this (http://chatelaine.cylabacademy.net:40392/47a0d.html) and click enter.
5. Then boom, we got the flag.
