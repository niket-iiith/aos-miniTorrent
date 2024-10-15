# P2P Group Based File Sharing System
 In this project, a simple 'BitTorrent' like P2P system for file download has been implemented. Its operation is based around the concept of a torrent file, a centralized tracker and an associated swarm of clients. A user (client) joins a P2P system by contacting the tracker. Any client in the network that is registered, can upload files in the network and download files from the network. clients which are online communicate with each other with the help of tracker. When multiple clients requesting for the same file, the publisher splits the file into chunks and different chunks are sent to each client, and the clients download the missing chunks from each other, thus both download time and load on the server is reduced. The clients select the chunk to be downloaded using piece selection algorithm. clients can upload file to another client as well as download from another client simultaneously.


## Prerequisites
##### Software Requirement

1. G++ compiler
   - *To install G++* : sudo apt-get install g++
2. OpenSSL library
    - *To install OpenSSL library* : sudo apt-get install openssl

*Platform*: Linux


## Compile code
##### tracker : 
>g++ tracker.cpp -o tracker -lssl -lcrypto

##### client :
>g++ client.cpp -o client -lssl -lcrypto -pthread


## Run code
##### Tracker
> `./tracker​ <TRACKER INFO FILE> <TRACKER NUMBER>`
> ex: ./tracker tracker_info.txt 1
##### Client
1. Run code
    > `./client​ <IP> <PORT> <TRACKER INFO FILE>
    > ex: ./client 127.0.0.1 5000 tracker_info.txt
2. Create user account:
    > create_user​ <user_id> <password>
3. Login:
    > login​ <user_id> <password>
4. Create Group:
    > create_group​ <group_id>
5. Join Group:
    > join_group​ <group_id> 
6. Leave Group:
    > leave_group <group_id>
7. List pending requests:
    > list_requests ​<group_id>
8. Accept Group Joining Request:
    > accept_request​ <group_id> <user_id>
9. List All Group In Network:
    > list_groups
10. List All sharable Files In Group:
    > list_files​ <group_id>
11. Upload File:
    > upload_file​ <file_path> <group_id​>
12. Download File:​
    > download_file​ <group_id> <file_name> <destination_path>
13. Logout:​
    > logout
14. Show_downloads: ​
    > show_downloads
15. Stop sharing: ​
    > stop_share ​<group_id> <file_name>


## Working
- clients are different instances of the same code client.cpp. 
- Each client/user should create an account and register with tracker. 
- Login using the user credentials. 
- Tracker maintains information of clients with their files(shared by client) to assist the clients for the communication between clients. 
- User can create Group and the one who created the group would become admin of that group. 
- User can fetch list of all Groups in server. 
- User can join/leave group. client should send request in order to join any group.  
- Only group admin can accept group join requests. 
- Upload file across group: Shares the filename and SHA1 hash of the complete file as well as piecewise SHA1 with the tracker. 
- Fetch list of all sharable files in a Group. 
- Download:  
    - Retrieve the list of clients sharing that file, from tracker. 
    - download file from multiple clients (different pieces of file from different clients - piece selection algorithm ) simultaneously and all the files which client downloads will be shareable to other users in the same group. File integrity is ensured using SHA1 comparison. 
- Piece selection algorithm used:  
- Show downloads. 
- Stop sharing file. 
- Logout - stops sharing all files. 
- Whenever client logins, all previously shared files before logout would automatically be on sharing mode. 
