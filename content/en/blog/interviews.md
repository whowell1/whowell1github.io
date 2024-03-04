---
author: "Wren Howell"
title: "Advice on Technical Interviews "
date: 2023-01-14
description: "Interviewing tips"
tags: ["Interview Questions Tips, Interview questions resources"]
thumbnail: https://image.cnbcfm.com/api/v1/image/107252082-1686077448227-job-interview-2021-09-24-04-13-49-utc.jpg?v=1688994001&w=630&h=354&ffmt=webp&vtcrop=y
---

 I have had mentees ask me for advice for technical interviews for a cyber security job. There is no question that the worst part of looking for a job is the interview because there is so much riding on your answers. To prepare, most beginners Google "Top 75 cybersecurity questions" and try to memorize questions from that list (links to some example questions are listed at the end).
 
 However, even though those questions are important to know, those questions do not really tell the interviewer of interviewee any essential information. These are the wrong questions to ask because they are Googleable questions. Somebody with no experience can memorize the questions, or a qualified candidate can forget the exact definition of these words in the heat of the moment. At a job, most WHAT questions can be Googled, and the actual work only starts when you can use the answers to formulate a theory and apply them. The purpose of a good interview should be to evaluate how prepared a candidate is for the job, and the questions asked should reflect questions that a candidate would be expected to answer. Here are some examples of bad interview questions: 

 
 **What is the difference between a trojan, a virus, and a worm?**

- A trojan is a malicious software that disguises itself as a legitimate program. Examples of Trojans are Infostealer and Emotet.  

- A virus is a type of malware that attaches itself to executable files or documents and replicates it by infecting other files. It typically requires user intervention to spread, such as running an infected program or opening an infected file. WannaCry is an example of a virus.


- A worm is a standalone malware program that spreads independently over computer networks or the internet, typically without user intervention. Unlike viruses, worms do not need to attach themselves to other files to spread. An example of a worm would be Stuxnet. 

**What is the difference between encryption, hashing, encoding, and serialization?**

- All four listed above are a way of changing the data from one form to another.  

- Encryption is a way to scramble data so only authorized parties can unscramble it. The only way to “unlock” a piece of data is to have a key. There are two types of encryption: public and private key encryption.
  - Public key encryption, also known as asymmetric encryption, is where something uses a public key to encrypt the message, and the recipient of the intended message uses the private key to decrypt the message. Examples are Diffie-Hellman key exchange and the RSA.  
  - Private key encryption or symmetric key encryption is the simple lock and key analogy. The same message is used to encrypt and decrypt a message. Examples that use this type of encryption are AES and WPA encryption.

- Hashing is the process of converting data — text, numbers, files — into a fixed-length string of letters and numbers. This form of data manipulation is not bidirectional, meaning that once you hash data using a hasing alogorithm, it is almost impossible to have the data return to its original form. Examples of hashes includes MD5 and sha256. 

- Encoding is converting one form of data to another so a different format can read it. An example would be encoding data from UTF-8 to another character set. Or converting data from json to xml. 

- Serialization refers to converting data from one structure to another for better storage or transmission. 

**What is the CIA triad?**

- The CIA triad is a model in cybersecurity that stands for confidentiality, integrity, and availability.
  - Confidentiality refers to the protection of sensitive information from unauthorized access or disclosure. This means ensuring that only authorized individuals or systems have access to certain data or resources.
  - Integrity ensures that data remains accurate, reliable, and consistent throughout its lifecycle. 
  - Availability ensures that information and resources are accessible and usable when needed by authorized users. 

**What is the DFIR process?**

- DFIR process is a structured method used in cybersecurity  to investigate and respond to cybersecurity incidents. The main steps are preparation, identification, containment, eradication, and lessons learned.

**What is the differences between the TCP/IP model and the OSI model?**
- This is also a better question as it interviewee to know the difference between the two models and the pros and cons of both. 
  - OSI Model has 7 layers. Here are the following layers starting from the bottom. They are:
    - Physical Layer: This layer is responsible for the physical transmission of data over the network medium. 
    - Data link Layers: This layer is responsible for the reliable transmission of data between adjacent nodes on the network.
    - Network Layer: This layer is responsible for the routing of data packets from the source to the destination across multiple network segments.
    - Transport Layer: This layer ensures reliable end-to-end communication between hosts on the network.
    - Session Layer: This layer establishes, manages, and terminates communication sessions between applications on different devices.
    - Presentation Layer:This layer is where data gets encrypted and decrypted and converted into a form that is accessible by the application layer.
    - Application Layer: This layer provides network services directly to end-users and applications
  
  - TCP/IP has 4 layers. Here are the following layerse starting from the bottom. They are
    - Application Layer: This layer interacts directly with end-users and provides network services such as email, file transfer, remote login, and web browsing. Examples of protocols here include DNS(Port 53), HTTP(Port 80), HTTPS(Port 443), SSH (Port 22). 
    - Transport Layer: This layer is responsible for end-to-end communication between the sender and receiver. Primary protocols in this layer is TCP and UDP. 
    - Internet Layer/Network Layer: The internet layer is responsible for routing packets across different networks to their destination. Primary protocol is IP. 
    - Link Layer/Network Interface Layer: This layer deals with the physical and logical connections between devices within the same network. Examples of protocols in this layer is Wifi and Ethernet. 

**What is the happens when you go type an url into a address bar?**

- This is a better question, as it requires you to know how people get to the Internet, but it is still easily googleable. [A good diagram to the answer.](https://github.com/whowell1/DFIR-Resources/blob/main/AddressBarGraphic.pdf)


Better interview questions will ask the interviewee about the situation and gauge how they would respond. Here are examples of better interview questions.  

- You have found three types of malware on different hosts: a trojan, a virus, and a worm. What are some ways to contain these types of malware?

- In what situations would a threat actor use encryption, hashing, and encoding to hide their malicious activities?

- In your opinion, what is the most essential part of the CIA triad?

These are better questions because they have a variety of answers that you can give that are not easily Googleable and require you to show nuance and situational awareness. My advice for those looking to interview would be say that understanding the WHAT questions are important, but more important are the how and why. When asked a situational question know how to explain why you are doing x and why you are doing y. 

**A link to resources that has a list of interview questions**

- Questions from [edureka](https://www.edureka.co/blog/interview-questions/cybersecurity-interview-questions/)

- Questions from [Simplilearn](https://www.simplilearn.com/tutorials/cyber-security-tutorial/cyber-security-interview-questions)

- Questions from [brainstation](https://brainstation.io/career-guides/cybersecurity-interview-questions)

{{< css.inline >}}

<style>
.emojify {
	font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
	font-size: 2rem;
	vertical-align: middle;
}
@media screen and (max-width:650px) {
  .nowrap {
    display: block;
    margin: 25px 0;
  }
}
</style>

{{< /css.inline >}}
