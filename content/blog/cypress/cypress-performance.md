---
title: Automated email testing with cypress
date: "2021-04-08T22:40:32.169Z"
description:
---

## Importance of automating your email testing

Despite all the disruptions in all the modes of communications, email is still the king when it comes to official relay of information. We rely on emails to receive bank alerts, important official email and often reports or alerts. It is very important to have proper coverage around the generated emails to make sure they work and appear as intended. 

## Set up 

For automated email testing, we will rely on an utility called [Mailosaur](https://mailosaur.com/docs/) with cypress

### Step 1: Create a mailosaur account
Make sure you know how to send email to Mailosaur first. Once you have this working, you’re ready to start testing.

### Step 2: importing and setting up mailsour npm package

```npm install cypress-mailosaur --save-dev```

in your ` cypress/support/commands.js` file, import `'cypress-mailosaur'` command. 

### Step 3: Add api key to `cypress.env.json` file.
```
{  
  "MAILOSAUR_API_KEY": "your-key-here"
}
```
### Step 4: Send email and verify

```
describe('Email Send test', () => {
    const serverId = 'SERVER_ID'; // Replace SERVER_ID with an actual Mailosaur Server ID
    const testEmail = `something@${serverId}.mailosaur.net`

    it('Send a sample email', () => {
        // Replace with cypress action which sends the email out. 
        cy.visit('mywebsite')
        cy.get('#email_field').type(testEmail)
        cy.get('#mybutton').click();
    })

    it('Gets a Password Reset email', () => {
        cy.mailosaurGetMessage(serverId, {
            sentTo: testEmail
        }).then(email => {
            expect(email.subject).to.equal('My message');
        })
    })
})
```

You can also test and verify sms as well which we will cover in the next post.