# AWS CLI, SDK, Cloud Shell

We have 3 options to access AWS:
- AWS Management Console *(protected by password + MFA)*
- AWS Command Line Interface(CLI) *(protected by access keys)*
- AWS software Developer Kit(SDK) *(for code: protected by access keys)*
- Access Keys are generated through aws console
- Users manage their own  access keys
- Access Keys are secret, just like a password. Dont share them
    - Access Key ID ~= username
    - Secret Access Key ~= password

## AWS CLI
- A tool that enables you to interact with AWS services using commands in your command-line shell
- Direct access to the public APIs of AWS sevices
- We can develop scripts to manage your resources
- It's open source https://github.com/aws/aws-cli
- Alternative to using AWS Management Console

## AWS SDK
- AWS Software Development Kit(AWS SDK)
- Language-specific APIs(set of libraries)
- Enables you to access and manage AWS services programmatically
- Embedded within you application
- Supports
    - SDKs(JavaScript, Python, PHP, .NET, Ruby, Java, GO, Node.js, C++)
    - Mobile SDKs(Android, iOS, ...)
    - IoT Device SDKs(Embedded C, Arduino, ...)
- Example: AWS CLI is built on AWS SDK for Python

### AWS Cloud Shell
- this is like CLI but in AWS management console
- only available in certain regions
