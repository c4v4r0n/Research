#  CVE-2024-26476 - OpenEMR Blind SSRF via HTML Injection in PDF Generator (mPDF)

Basically there is no input sanitization in the PDF content that is generated in interface/procedure_tools/labcorp/ereq_form.php.
For example we can use the $form_id variable (line 20) to inject an img tag with the src attribute that points to a server we control.

https://nvd.nist.gov/vuln/detail/CVE-2024-26476

Product: https://www.open-emr.org/

Vulnerable: version < 7.0.2

Vector: A authenticated user must request interface/procedure_tools/labcorp/ereq_form.php with a XSS payload in the formid parameter to insert a malicious img tag

```
http://10.211.55.9/openemr/interface/procedure_tools/labcorp/ereq_form.php?debug=true&formid=<img src="http://10.37.129.2">
```

![image](https://github.com/c4v4r0n/Research/assets/57950943/adae8062-13d5-4f24-ab4d-8aea64e211aa)

Reported by Vinicius Silva on 02/13/2024

Fixed in: 02/14/2024 - https://github.com/openemr/openemr/commit/846301aaa798839025cfb3cf3d58dbfda1e4e5ba
