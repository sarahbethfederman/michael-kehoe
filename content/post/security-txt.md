+++
author = ""
date = "2019-07-03T20:00:00-08:00"
draft = false
title = "Security.txt"
slug = "security-txt"
tags = ["security"]
image = "img/main/cover2.jpg"
comments = true     # set false to hide Disqus comments
share = true        # set false to hide share buttons
menu = ""           # set "main" to add this content to the main menu
+++
`security.txt` is a draft IETF standard for websites (webmasters) to communicate security vulnerability/ research policy. The purpose of the standard is to communicate in a standardized manner. The abstract of the RFC states:
>  When security vulnerabilities are discovered by independent security
   researchers, they often lack the channels to report them properly.
   As a result, security vulnerabilities may be left unreported.  This
   document defines a format ("security.txt") to help organizations
   describe the process for security researchers to follow in order to
   report security vulnerabilities.

# Specification
The `security.txt` file contains seven fields:

1. Acknowledgements: This directive allows you to link to a page where security researchers are recognized for their reports. The link MUST begin with "https://".
2. Canonical: This directive indicates the canonical URI where the security.txt file is located. The link MUST begin with "https://".
3. Contact: This directive allows you to provide an address that researchers SHOULD use for reporting security vulnerabilities.  The value MAY be an email address, a phone number and/or a web page with contac information. This directive MUST be present in a security.txt file. The link MUST begin with "https://".
4. Encryption: This directive allows you to point to an encryption key that security researchers SHOULD use for encrypted communication. The link MUST begin with "https://".
5. Hiring: The "Hiring" directive is used for linking to the vendor's security-related job positions.
6. Policy: This directive allows you to link to where your security policy and/ or disclosure policy is located. The link MUST begin with "https://".
7. Prefered-Languages:  This directive can be used to indicate a set of natural languages that are preferred when submitting security reports.  This set MAY list multiple values, separated by commas.

Web-based services should place the security.txt file under the `/.well-known/` path; e.g. `https://example.com/.well-known/security.txt`

# Example(s)
* https://www.google.com/.well-known/security.txt
* https://www.facebook.com/.well-known/security.txt
* https://securitytxt.org/.well-known/security.txt


You can find the current RFC draft [here](https://github.com/securitytxt/security-txt/blob/master/draft-foudil-securitytxt.txt)
