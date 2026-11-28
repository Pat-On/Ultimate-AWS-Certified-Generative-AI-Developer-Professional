# 212. IAM Users & Groups - Hands On

## IAM is global

In the IAM console the region selector shows **Global**: users exist in every region, while many other consoles are region specific.

## Why create a user

The account starts with the **root user** (the top-right menu shows only the account ID). Daily work should use another user, such as an administrator.

## Create the user

1. IAM → **Users** → create, with **console access**.
2. AWS recommends **IAM Identity Center**; the course creates an **IAM user** (simpler, and what the exam asks about).
3. Password: for another person, **auto-generated** and **changed at first sign-in**; for yourself, a custom one.
4. Permissions: create the group **`admin`** with the **`AdministratorAccess`** policy and add the user to it.
5. Optional **tags** add metadata (for example `department = engineering`).
6. Email the sign-in instructions or download the **CSV**.

The user's permissions show `AdministratorAccess` as **inherited from the group**, not attached directly. Groups make permissions easier to manage.

## Sign in

- The dashboard shows the **account ID** and **sign-in URL**; an **account alias** (globally unique) simplifies the URL.
- On the sign-in page choose **IAM user** and give the account ID or alias, user name and password.
- A **private browser window** lets you keep root and the IAM user signed in side by side.

**Do not lose** the root or administrator credentials; recovery needs AWS Support. Prefer the IAM user for the course.

## Exam takeaways

1. Do not use **root** for daily work.
2. Attach policies to **groups**; users **inherit** them.
