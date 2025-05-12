# Lab 1 : Breach in the cloud.

## Here i will mention all the following steps to perform the lab and get the flag.

- <ins>Step 1</ins> : Download the CloudTrail logs in INCIDENT-3252.zip from the 🔎-case-files channel in the Pwned Labs [Discord Link](https://discord.gg/pwnedlabs).<br/>
* <ins>Step 2</ins> : **Understanding CloudTrail** : CloudTrail is a service that records and monitor activities and events within the AWS Cloud Environment! :shipit: 
And it captures a detailed history of actions taken by users, roles and any AWS services :eyes:. CloudTrail logs include information such as who performed an action, what action was taken by the user or role or service. It also enables users to better understand and manage their AWS Infrastructure.
![This image shows the structure of the logfile name](https://github.com/user-attachments/assets/a54f40e6-986e-4d8b-a4e7-7b557fc9d2e3)
![TimeStamp Structure](https://github.com/user-attachments/assets/6990e04a-dd01-4e82-ad82-9903135d94e3)

* <ins>Step 3</ins> : Now first we need to unzip the file and store the files in the directory. Use command: <code>unzip filename.zip -d newFile</code>
![image](https://github.com/user-attachments/assets/03d83f02-826d-409f-afa1-a0dae438520e)

- <ins>Step 4</ins> : Then you need to use command: <code>apt install jq</code>.
- <ins>Step 5</ins> : Then run the following command: <code>for file in *.json; do jq . "$file" > "$file.tmp" && mv "$file.tmp" "$file"; done</code> inside the directory where the .json files are present.
![image](https://github.com/user-attachments/assets/00ec84b8-b9ec-4519-a0c7-10b421a2a8f8)
- <ins>Step 6</ins> : Now use command: <code> grep -r userName | sort -u </code>
![image](https://github.com/user-attachments/assets/2ced3a50-cca6-488d-9e8a-cca8fea0cb1a)

- <ins>Step 7</ins> : Now use command: <code>cat 107513503799_CloudTrail_us-east-1_20230826T2* | jq > full-logs.json</code>
- <ins>Step 8</ins> : Now use command: <code>grep -A 10 temp-user full-logs.json</code>
![image](https://github.com/user-attachments/assets/b7f5f93c-a5c1-431d-a8d8-03bbca02e664)

- <ins>Step 8</ins> : Now take a IP and check from where it is comming from

![image](https://github.com/user-attachments/assets/9552c9ee-941e-4328-be4a-a6ab8945129d)
![image](https://github.com/user-attachments/assets/d105b221-4c4e-4733-8421-454a52300c9d)


- <ins>Step 9</ins> : Now here they are trying to perform privilege escalation.
![image](https://github.com/user-attachments/assets/1a373fe6-32d1-45e4-81fa-03765d2444b5)


- <ins> Step 10 </ins> : Now use command: <code>cat full-logs.json | grep -A 40 MySession </code>. Then you will see the following.
![image](https://github.com/user-attachments/assets/694ed8e1-633b-45fc-99ec-3781d562a2c1)

- <ins>Step 11</ins>: Then they downloaded from the emergency-bucket

![image](https://github.com/user-attachments/assets/0e53e430-d13c-4700-9f7b-386f4f4bb76d)


Now retracting steps as an attacker
- aws configure
- aws sts get-caller-identity

![image](https://github.com/user-attachments/assets/abf5f130-f6c2-40b0-a725-ae2e1a8bbf3c)

- aws iam list-user-policies --user-name temp-user

![image](https://github.com/user-attachments/assets/66645b82-a021-4c95-97c8-e1f108f6c406)

- aws iam get-user-policy --user-name temp-user --policy-name test-temp-user

![image](https://github.com/user-attachments/assets/b5dddc95-ff44-448c-a822-1c4685c8e57c)

- aws sts assume-role --role-arn arn:aws:iam::107513503799:role/AdminRole --role-session-name MySession

![image](https://github.com/user-attachments/assets/48d87395-4f3a-461a-8ad8-f86c5bbaeefa)

Now do the following

![image](https://github.com/user-attachments/assets/4c00cee4-7bfd-4a84-b971-bf7eab34d8b2)


