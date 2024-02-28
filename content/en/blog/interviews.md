---
author: "Wren Howell"
title: "Advice on Technical Interviews "
date: 2023-01-14
description: "Interviews"
tags: ["Interview Questions"]
thumbnail: https://image.cnbcfm.com/api/v1/image/107252082-1686077448227-job-interview-2021-09-24-04-13-49-utc.jpg?v=1688994001&w=630&h=354&ffmt=webp&vtcrop=y
---

 I have had mentees ask me for advice for technical interviews for a cyber security job. There is no question that the worst part of looking for a job is the interview because there is so much riding on your answers. To prepare, most people Google "Top 75 cybersecurity questions" and try to memorize questions from that list (links to some example questions are listed at the end).
 
 However, even though those questions are important to know, those questions do not really tell the interviewer of interviewee any essential information. These are the wrong questions to ask because they are Googleable questions. Somebody with no experience can memorize the questions, or a qualified candidate can forget the exact definition of these words in the heat of the moment. At a job, most WHAT questions can be Googled, and the actual work only starts when you can use the answers to formulate a theory and apply them. The purpose of a good interview should be to evaluate how prepared a candidate is for the job, and the questions asked should reflect questions that a candidate would be expected to answer. Here are some examples of bad interview questions: 

 
 **What is the difference between a trojan, a virus, and a worm?**

- A trojan is a malicious software that disguises itself as a legitimate program. Examples of Trojans are Infostealer and Emotet.  

- A virus is a type of malware that attaches itself to executable files or documents and replicates it by infecting other files. It typically requires user intervention to spread, such as running an infected program or opening an infected file. WannaCry is an example of a virus.


- A worm is a standalone malware program that spreads independently over computer networks or the internet, typically without user intervention. Unlike viruses, worms do not need to attach themselves to other files to spread. An example of a worm would be Stuxnet. 

**What is the difference between encryption, hashing, encoding, and serialization?**

- All four listed above are a form of changing the data from one form to another.  

- Encryption is a way to scramble data so only authorized parties can unscramble it. The only way to “unlock” a piece of data is to have a key. There are two types of encryption: public and private key encryption.
  - Public key encryption, also known as asymmetric encryption, is where something uses a public key to encrypt the message, and the recipient of the intended message uses the private key to decrypt the message. Examples are Diffie-Hellman key exchange and the RSA.  
  - Private key encryption or symmetric key encryption is the simple lock and key analogy. The same message is used to encrypt and decrypt a message. Examples that use this encryption are AES and WPA encryption.

- Hashing is the process of converting data — text, numbers, files — into a fixed-length string of letters and numbers. This form of data manipulation is not bidirectional, meaning that once you hash data using a hasing alogorithm, it is almost impossible to have the data return to its original form. Examples of hashes includes MD5 and sha256. 

- Encoding is converting one form of data to another so a different format can read it. An example would be encoding data from UTF-8 to another character set. Or converting data from json to xml. 

- Serialization refers to converting data from one structure to another for better storage or transmission. 

**What is the CIA triad?**

- The CIA triad is a model in cybersecurity that stands for confidentiality, integrity, and availability.
  - Confidentiality refers to the protection of sensitive information from unauthorized access or disclosure. This means ensuring that only authorized individuals or systems have access to certain data or resources.
  - Integrity ensures that data remains accurate, reliable, and consistent throughout its lifecycle. 
  - Availability ensures that information and resources are accessible and usable when needed by authorized users. 

**What is the DFIR process?**

- DFIR process is preparation, identification, containment, eradication, and lessons learned.
 
Better interview questions will ask the interviewee about the situation and gauge how they would respond. Here are examples of better interview questions.  

**You have found three types of malware on different hosts: a trojan, a virus, and a worm. What are some ways to contain these types of malware?**

**In what situations would a threat actor use encryption, hashing, and encoding to hide their malicious activities?**

**In your opinion, what is the most essential part of the CIA triad?** 

These are better questions because they have a variety of answers that you can give that are not easily Googleable and require you to show nuance and situational awareness. 

**A link to resources that a list of interview questions**

[Simplilearn] (https://www.simplilearn.com/tutorials/cyber-security-tutorial/cyber-security-interview-questions)
[edureka]  (https://www.edureka.co/blog/interview-questions/cybersecurity-interview-questions/)
[brainstation] (https://brainstation.io/career-guides/cybersecurity-interview-questions)

We just updated our [Docs Contribution Guide](https://www.codecademy.com/pages/contribute-docs)!




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
