---
title: "Password Complexity for Zod - Next.js - Code with Mosh Forum"
source: "https://forum.codewithmosh.com/t/password-complexity-for-zod/23622"
author:
  - "[[Code with Mosh Forum]]"
published: 2023-11-14
created: 2025-03-05
description: "const schema = z  .object({    email: z.string().email(),    password: z.string().min(8),  })  .superRefine(({ password }, checkPassComplexity) =&gt; {    const containsUppercase = (ch: string) =&gt; /[A-Z]/.test(ch);  &hellip;"
tags:
  - "clippings"
---
```auto
const schema = z
  .object({
    email: z.string().email(),
    password: z.string().min(8),
  })
  .superRefine(({ password }, checkPassComplexity) => {
    const containsUppercase = (ch: string) => /[A-Z]/.test(ch);
    const containsLowercase = (ch: string) => /[a-z]/.test(ch);
    const containsSpecialChar = (ch: string) =>
      /[\`!@#$%^&*()_\-+=\[\]{};':"\\|,.<>\/?~ ]/.test(ch);
    let countOfUpperCase = 0,
      countOfLowerCase = 0,
      countOfNumbers = 0,
      countOfSpecialChar = 0;
    for (let i = 0; i < password.length; i++) {
      let ch = password.charAt(i);
      if (!isNaN(+ch)) countOfNumbers++;
      else if (containsUppercase(ch)) countOfUpperCase++;
      else if (containsLowercase(ch)) countOfLowerCase++;
      else if (containsSpecialChar(ch)) countOfSpecialChar++;
    }
    if (
      countOfLowerCase < 1 ||
      countOfUpperCase < 1 ||
      countOfSpecialChar < 1 ||
      countOfNumbers < 1
    ) {
      checkPassComplexity.addIssue({
        code: "custom",
        message: "password does not meet complexity requirements",
      });
    }
  });
```