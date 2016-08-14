---
layout: post
category : lessons
tagline: "shell"
tags : [shell]
---
{% include JB/setup %}

Python  is a strong script language. today, we are going to use is to fetch the email
with pop3.

###python script
    import poplib  
    import email

    # emailServer.set_debuglevel(1)//This is for debug 

    emailServer = poplib.POP3('pop.163.com')  
    emailServer.user('xxxxxx@163.com')  
    emailServer.pass_('xxxxxxxx)  

    emailMsgNum, emailSize = emailServer.stat()
    print 'email number is %d and size is %d'%(emailMsgNum, emailSize)  

    for i in range(1, emailMsgNum+1):  
        hdr, message, octet = emailServer.retr(i)
        # print message        
        mail = email.message_from_string('\n'.join(message))
    
        # print mail.get('subject')
        # print mail.get('from')
        # print mail.get('to')
        # for header in ('From','To','Subject'):
        #     if header in mail:
        #         print mail[header]
        print mail.get('Subject')
        #"=?ISO-8859-1?B?VGFuZyxBbGxlbg==?=" <chuanzhou.tang@foxmail.com>
        print mail.get('From').split(' ')[1]
        print mail.get('To').split(' ')[1]

        # prints the raw text
        for part in mail.walk():
        # each part is a either non-multipart, or another multipart message
        # that contains further parts... Message is organized like a tree
            if part.get_content_type() == 'text/plain':
                print part.get_payload(None, True)                                        
    emailServer.quit()

###Some Summary
when fetching the from and to info from the email, seems there is some coded message 
before, so we split and get the message we want.


