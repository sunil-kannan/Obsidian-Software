---
date: 2024-11-01
tags: 
link: "[[Core Java]]"
---

# Coupling & Cohesion

>Coupling and Cohesion are important factors in determining the maintainability, scalability, and reliability of a software system. High coupling and low cohesion can make a system difficult to change and test, while low coupling and high cohesion make a system easier to maintain and improve.

## Coupling

**Coupling** refers to the degree of interdependence between software modules. **High coupling** means that modules are closely connected and changes in one module may affect other modules. **Low coupling** means that modules are independent, and changes in one module have little impact on other modules.

### Example 
#### High coupling / Tight coupling
```java
class Main {
    public static void main(String[] args) {
        OtpManager otpManager = new OtpManager();
        otpManager.sendOtp("193783");
    }
}

class OtpManager {
    // Directly depends on Email class
    private Email emailService = new Email();

    public boolean sendOtp(String otp) {
        String content = "Your otp is " + otp;
        sendOtpThroughEmail(content);
        return true;
    }

    // Directly uses Email instance
    public boolean sendOtpThroughEmail(String content) {
        //send email using the emailService
        System.out.println("Sending email: " + content);
        return true;
    }
}

class Email {
    // Email sending logic
}

```

- Incase in future if you are going to implement the sending otp through mobile means it will be difficult because it is dependent and it is tight coupling.
- In below example you will see low coupling.
#### low coupling / Loose coupling

```java


class Main { 
	public static void main(String[] args) {  
		EmailService emailService = new EmailService(); 
		OtpManager otpManager = new OtpManager(emailService); 
		otpManager.sendOtp("193783"); 
		MobileService mobileService = new MobileService(); 
		OtpManager otpManager1 = new OtpManager(mobileService); 
		otpManager1.sendOtp("193783"); 
	}
}

// Define an interface for sending OTP  
interface OtpSender {  
    boolean sendOtp(String content);  
}  
  
// Implement the OtpSender interface in EmailService  
class EmailService implements OtpSender {  
    @Override  
    public boolean sendOtp(String content) {  
        //send email logic  
        System.out.println("Sending email: " + content);  
        return true;  
    }  
}  
  
class OtpManager {  
    private final OtpSender otpSender; // Dependency is passed in  
  
    // Constructor injection    public OtpManager(OtpSender otpSender) {  
        this.otpSender = otpSender;  
    }  
  
    public boolean sendOtp(String otp) {  
        String content = "Your otp is " + otp;  
        otpSender.sendOtp(content); // Use the abstracted service  
        return true;  
    }  
}  
  
// Mobile class remains unchanged  
class MobileService implements OtpSender {  
    @Override  
    public boolean sendOtp(String content) {  
        //send email logic  
        System.out.println("Sending message: " + content);  
        return true;  
    }  
}
```
### Cohesion

Cohesion in Java is the Object-Oriented principle most closely associated with making sure that a class is designed with a single, well-focused purpose. In object-oriented design, cohesion refers to how a single class is designed.