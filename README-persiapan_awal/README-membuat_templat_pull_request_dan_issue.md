# Membuat templat *pull-request* dan *issue*
Berikut ini adalah referensi untuk membuat keduanya:
- [Pembuatan templat *pull-request*](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)[^1]
- [Pembuatan dan Konfigurasi templat *issue*](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)[^2]

Berikut ini adalah bentuk templat *pull-request* di repositori ini:

```markdown
<!-- Use this guide before creating pull-request: https://github.blog/2015-01-21-how-to-write-the-perfect-pull-request/#approach-to-writing-a-pull-request -->
<!-- Basic markdown syntax on Github: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax#using-emoji -->
## Description
Describe the changes you've made
- This is a spike to explore…
- This simplifies the display of…
- This fixes handling of…

## List of Changes
Create a list with these bullets for:

\+ (plus_sign) indicates that you add something

\- (minus_sign) indicates that you remove something

\~ (tilde_sign) indicates you change something

Add a backslash (\\) to ignore markdown rendering and newline  after each list.

## Refference to issue
- close #12 - explanation about the linking issue
- fix #12 - explanation about the linking issue
- resolve #12 - explanation about the linking issue

<!-- find more info about linking issue to pull-request: https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue -->


<!-- Mention anybody to review, discuss, or accept this pull-request (If any). Ask them politely and type why they should do that. -->

```

Pada templat di atas, saya menambahkan referensi untuk mempelajari bagaimana cara membuat pull-request yang baik.

Saya membuat 2 templat issue untuk membuat laporan bug (*bug report*) dan templat user-story untuk mengumpulkan kebutuhan pengguna.

Templat `bug-report` saya pakai dari bawaan milik Github seperti ini bentuknya:

```markdown
**Describe the bug**
A clear and concise description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '....'
3. Scroll down to '....'
4. See error

**Expected behavior**
A clear and concise description of what you expected to happen.

**Screenshots**
If applicable, add screenshots to help explain your problem.

**Desktop (please complete the following information):**
 - OS: [e.g. iOS]
 - Browser [e.g. chrome, safari]
 - Version [e.g. 22]

**Smartphone (please complete the following information):**
 - Device: [e.g. iPhone6]
 - OS: [e.g. iOS8.1]
 - Browser [e.g. stock browser, safari]
 - Version [e.g. 22]

**Additional context**
Add any other context about the problem here.

```

Templat `user-story`:

```markdown
Write your user story here.

<!-- example: As a manager, I want to be able to understand my colleagues progress, so I can better report our sucess and failures.  -->

## More Information
<!-- Explain more further about the story -->
### As a [the Who/Role]
Describe yourself or the user that have this requirement.

### I want/want to/need/can/would like [the What/Goal]
Describe the requirement, the need, or the goal wants to accomplish.

### So that [the Why/Benefit]
The benefit wants to get.

### Screenshot or Drawing Sketch
Place your sketch about the requirement here.

```

[^1]:Github. (2023, February 15). _Creating a pull request template for your repository_ [Documentation]. GitHub Docs. [https://ghdocs-prod.azurewebsites.net/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository](https://ghdocs-prod.azurewebsites.net/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)
[^2]:Github. (2023, March 30). _Configuring issue templates for your repository_ [Documentation]. GitHub Docs. [https://ghdocs-prod.azurewebsites.net/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository](https://ghdocs-prod.azurewebsites.net/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository)
