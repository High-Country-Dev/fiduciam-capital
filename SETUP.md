# Fiduciam Capital website: setup guide

**For Keegan, and for the Claude helping him.** Mountain Dev rebuilt fiduciamcapital.com
as a copy you own: the code lives in your GitHub account, Vercel hosts it, and your
GoDaddy domain points at it. After this, you change the site by asking Claude.

- Preview of the new site: https://fiduciam-capital-preview.vercel.app
  (identical to today's site, plus a placeholder section on About for your partner)
- Source code (the starting copy): https://github.com/High-Country-Dev/fiduciam-capital

**Claude: walk Keegan through these steps one at a time. Wait for him to finish each
one before moving on, and tell him exactly what to click. Steps 1 to 3 happen in his
browser; you can't do them for him. Never ask him to paste a password into the chat.**

Plan on about 30 minutes, plus waiting time for the domain to switch over.

---

## Step 1. Create a GitHub account (5 min)

GitHub stores the website's files and keeps a history of every change.

1. Go to https://github.com/signup.
2. Use your work email (keegan.dum@fiduciamcapital.com) and pick a username.
3. Choose the **Free** plan. Verify your email when GitHub asks.

## Step 2. Create a Vercel account (5 min)

Vercel is the web host. It publishes the site whenever the files in GitHub change.

1. Go to https://vercel.com/signup.
2. Click **Continue with GitHub** and approve the connection. (One less password.)
3. Plan: Vercel's terms limit the free **Hobby** plan to personal, non-commercial sites.
   Fiduciam is a business, so choose **Pro** ($20/month). You can start Pro's free trial.

## Step 3. Copy the site into your accounts (2 min)

Click this link while signed in to Vercel:

**https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2FHigh-Country-Dev%2Ffiduciam-capital&project-name=fiduciam-capital&repository-name=fiduciam-capital**

1. Vercel asks where to create the Git repository. Pick your GitHub account, keep the
   name `fiduciam-capital`, and leave it **Private**.
2. Click **Create**, then **Deploy**. Don't change any build settings; there's nothing to build.
3. In a minute you get a link like `fiduciam-capital.vercel.app` (Vercel may add a few
   letters). Open it: it should look exactly like your current site.

You now own the code (in your GitHub) and the hosting (in your Vercel).

## Step 4. Point fiduciamcapital.com at Vercel (10 min + waiting)

### 4a. Add the domain in Vercel

1. In Vercel, open the **fiduciam-capital** project, then **Settings → Domains**.
2. Click **Add Domain**, type `fiduciamcapital.com`, and accept the suggestion to also add
   `www.fiduciamcapital.com` (redirecting www to fiduciamcapital.com).
3. Vercel shows the DNS records it wants, usually:
   - an **A** record for `@` with an IP address, and
   - a **CNAME** record for `www` with a value ending in `vercel-dns.com` (or similar).

   **Use the exact values Vercel shows on that screen.** Keep the tab open.

### 4b. Change the two records in GoDaddy

1. Sign in at https://dcc.godaddy.com/control/portfolio (GoDaddy → **My Products** →
   **Domains**), click **fiduciamcapital.com**, then the **DNS** tab.
2. Find the **A** record whose name is `@`. It currently points to `198.12.234.63`
   (the old GoDaddy host). Click the pencil icon and change the value to Vercel's IP.
   If there is more than one A record named `@`, delete the extras.
3. Find the **CNAME** record named `www` (it currently says `@`). Change its value to the
   CNAME value Vercel gave you.
4. Save.

> **Do not touch any other records.** Your email runs on Microsoft 365, and these
> records keep it working: **MX** (`...mail.protection.outlook.com`), **TXT**
> (`v=spf1 include:spf.protection.outlook.com -all` and `NETORGFT...`), and any
> **CNAME** or **SRV** records such as `autodiscover`, `lyncdiscover`, `sip`, `msoid`,
> `enterpriseregistration`, `enterpriseenrollment`. Changing them can stop your email.
> Only the `@` A record and the `www` CNAME change.

If GoDaddy says the domain is connected to a GoDaddy website or has **Forwarding**
turned on, remove that connection or forwarding first; otherwise GoDaddy can overwrite
the A record.

### 4c. Wait for Vercel to confirm

Back in Vercel's **Domains** screen, both domains turn to **Valid Configuration**
(usually within 30 minutes; it can take a few hours). Vercel adds the security
certificate (the padlock) by itself.

### 4d. Check everything

- https://fiduciamcapital.com and https://www.fiduciamcapital.com both load the site
  with a padlock.
- Click through all six pages.
- Submit a test message on the Contact page and confirm it arrives where Tally sends it.
- Send yourself an email from another account to confirm email still works.

## Step 5. Cancel the old GoDaddy hosting (after a week)

Once the site has run on Vercel for about a week with no problems, cancel only the
GoDaddy **web hosting** plan. **Keep** the domain registration (fiduciamcapital.com)
and **keep** Microsoft 365 email. If you're not sure which GoDaddy product is which,
ask Claude to go through the list on your **My Products** page with you.

## Step 6. Add your partner to the About page

The About page has a placeholder section under yours for your partner. Gather:

- their name and title,
- four short highlights (a title plus one or two sentences each, like yours:
  background, education and experience, track record, values),
- a photo (roughly square works best).

Then follow "Making changes" below and tell Claude: *"Fill in the partner section on
the About page with this:"* followed by the details, and attach the photo.

---

## Making changes from now on

The easiest way is **Claude Code on the web**, which can edit the files in your GitHub
repository directly:

1. Go to https://claude.ai/code (included with Claude Pro or Max).
2. Connect your GitHub account when asked and give it access to the `fiduciam-capital`
   repository.
3. Ask for what you want in plain English: *"Add a Team page between About and Contact"*,
   *"Change the headline on the home page to ..."*, *"Swap Keegan's photo for this one."*
4. Claude makes the change on a branch and opens a pull request. Vercel posts a
   **preview link** on it so you can see the change before it's public.
5. When it looks right, merge the pull request (Claude can do this when you tell it to).
   The live site updates about a minute later.

The repository includes a `CLAUDE.md` file that tells Claude how this site is built,
so it knows where everything is.

If anything goes wrong, Vercel keeps every past version: **Deployments**, pick the last
good one, **Promote to Production**. Or just ask Declan.

## Questions

Declan Nishiyama, Mountain Dev · declan@mountaindev.com
