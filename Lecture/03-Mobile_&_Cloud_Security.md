# Mobile & Cloud Computing
## Software Security Lab
### Research Area
- Blockchain Security
    - An Empirical Study of NFT Scams in Discord (in submission)
    - EtherDiffer: Differential Testing on RPC Services of Ethereum NOdes (FSE 2023)
- Android Security
    - Security of Android Platform (SPE 2017)
    - Static Analysis of Android App (ASE 2017)
    - Security Analysis of ADB (Asia's 2015)
- Binary Analysis
    - Readability Metric for Decompiled Code
    - Firmware Re-hosting Techniques
- Web Security
    - Security ANalysis of REST API
- Phishing / Darkweb
    - Analysis of Phishing Attacks and Cybercrime Marketplace
- Cloud Security
    - Security Analysis of Kubernetes Policies
    - Automated Testing Framework for Virtual Machine (ICSE 2021)
- Automotive Security
    - Dynamic Analysis of Automotive SW

## Research 1
### Background: Activity Task
- No access control if malware task injected

### Activity Injection Attack: Demo
1. Facebook Task
2. Launch malware
3. Seems normal, but silently injects a malicious Facebook login activity into the Facebook app's task.
4. Back to home screen
5. Go back to Facebook
6. Malicious Facebook login activity is shown on the screen, instead of normal one

> Malicious Injection doesn't require special permission

### Activity Activation Rules
- Depends on complex combinations of flags and launchModes
1. Launch mode
2. Intent Flag
3. Task Affinity 

- Among 239 Rules, found 180 conditions for activity injection

### Detection Tool
1. APK
2. Activity Info Extractor | CHA CallGraph Builder
3. Activity Info. | CallGraph
4. Intent Analyzer
5. Intent Data
6. Activity Injection Detector
7. Injection Report

### Evaluation
1. Total Apps: 129,756
2. Possible to inject: 4,763
3. Analysis in Time: 4,633
4. Injection Detected: 1,761

## Research 2
### Java Native Interface
- All JVMs follow the JNI specification
- Sequence of API calls
    - GetObjectClass
    - GetMethodID
    - CallObjectMethod
> It is easy to go wrong in JNI program
> Does JVM validate invalid usage of JNI functions?

### Unspecified Cases
- clazz: a subclass of java.lang.Throwable, must not be NULL
- What happens if non-Throwable object is passed?

### JUSTGEN
- testing framework
- provide JNI specification
    - then converted into JNI spec. in DSL
- uses SMT solver
    - tool to find answers for boolean
- Creates Test program
- Found 34,990 Unspecified Cases

### Validation Capability of JVMs
- When you see that a certain JNI function must receive a non-NULL object, `It is your responsibility` to ensure that NULL is not passed to that JNI function

- As a result, a JNI implementation does not need to perform NULL pointer checks

### Xcheck:jni
- this option causes the VM to do additional validation on the arguments passed to JNI functions

### Evaluation Result
- from 34,990 Unspecified Cases
- 4 different categories:
    - Misbehave
        - Case terminate normally without warning
        - each running may produce different results
    - SegFault
        - causes segmentation fault error
    - Exception
        - causes exception error
    - Validation
        - Successful

- Exception and validation are good
- Misbehave and segfault is a problem

### Finding 1: Error handling issues 
- Error handling using return values of JNI functions is not reliable
- parameter should be greater than 0
- When given a negative value, all JVMs could not validate negative values
- Does not return failure value or warning message, it gives weird values

#### Evaluation Result
- Segmentation Fault
    - JVM crashing
- Missing type Check: using incorrect type
- Missing Null check: using null values
- missing liveness check: using objects
- missing releasable check: releasing unreleasable objects

- Some test cases, all JVMs could not validate

- 792 unspecified cases, and 563 unspecified cases are fixed by OpenJ0

## Android Auto
- security issues in automotives
- develop automated techniques to verify software running on android auto (ECU)

### Environment Setup
- Hyundai IVI System
    - SONATA
    - SANTA FE
    - GENESIS

### Test ECU