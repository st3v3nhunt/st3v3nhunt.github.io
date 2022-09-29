---
title: "☁️  Hosting GOV.UK prototypes"
date: "2022-09-29"
tags: ["gov.uk", "prototypes", "heroku", "hosting"]
categories: ["development"]
---

Whenever I have used the
[GOV.UK Prototype Kit](https://govuk-prototype-kit.herokuapp.com/)
to build a prototype I have always hosted it on
[Heroku](https://www.heroku.com/). The main reason for doing this was because
it was just so easy (I wrote a
[post](./posts/how-to-setup-a-simple-heroku-pipeline/) about just how easy it
was many years ago), it was also the default approach - until recently.

## Heroku's next chapter

At the end of August 2022 Heroku
[communicated](https://blog.heroku.com/next-chapter) they were going to be
> phasing out our free plan for Heroku Dynos

Unfortunately this was the plan used for all of the prototypes I had setup and
I would imagine almost all of the other GOV.UK prototypes running on the
platform too (although I have no data to back this up).

The best thing about it being free was that you could get it setup with a
personal account, get working on it quickly and then not worry about how long
it might take to go through the discussions internally about who and how it
would be managed and maintained. Because it wasn't going to cost you
anything it didn't matter if those discussions took some time or indeed, if
they never happened at all (which isn't necessarily the best idea but in
reality a prototype should be perfectly OK being managed by the team doing the
work with the prototype).

Since the initial announcement, Heroku have said they will
[introduce a new low-cost plan](https://blog.heroku.com/new-low-cost-plans)
called `Eco`, providing 1000 hours across all Eco dynos for $5 a month. So
if you wanted to continue to use Heroku it isn't going to cost much,
although you might need to go through the red tape and discussions to get it
paid for!

In all seriousness, if you are already using Heroku, the easiest and most
effective option _should_ be to just go for a paid for plan.

## Alternative hosting providers

With the plan changes and the nuisance a security incident in [April 2022](https://status.heroku.com/incidents/2413) when
[GitHub Integration](https://blog.heroku.com/github-integration-update) with
Heroku was disabled caused, I had been considering trying alternatives to
Heroku.

Plus, this sort of stuff is interesting and good to look at every so often! So,
if you wanted to use another hosting provider (why not try something
different, you might like it 😃) there are several to choose from.

GOV.UK suggests:

- [Railway](https://railway.app/new/github)
- [Render](https://render.com/docs/github)

I've tried both to see what they were like, below is a short summary of what I
found. Note that this is not a detailed comparison and doesn't consider the
paid offering, I really just wanted to see what you could get for free.

### Railway

Railway is very easy to
[get started](https://docs.railway.app/getting-started) with due to the
GitHub app integration.

During the deployment flow you are asked if there are
any environment variables you want to setup. For a GOV.UK prototype there are
two env vars that should be set:

- `NODE_ENV=production` - sets the runtime environment to `production` which
  will result in a password being required to access the site
- `PASSWORD=<whatever_you_want>` - sets the password to access the site

A note on the password - it is important to set `NODE_ENV=production`. Without
this the application will not prompt for a password. And you **really** want a
password prompt to protect people and prevent them from stumbling across the
prototype and potentially mistaking it for a real service.

After running through the deploy flow and setting the env vars the site was
running as expected - very straightforward.

A draw back of Railway is, on the
[Starter Plan](https://docs.railway.app/reference/plans) the service is limited
to running for 500 hours which isn't enough to run all day every day. This
wouldn't be a problem if the service could easily be stopped and started when
needed, however (at the time of writing) I can't see a way to do this beyond
removing the service and then adding it back.

The process is reasonably
straight forward and if it could be automated it wouldn't really be an issue
but the [CLI](https://docs.railway.app/reference/cli-api) doesn't appear to
provide the ability to do this. It ends up being a bit of a nuisance as
the env vars (and other data) are deleted each time resulting in a
manual process taking ~5 mins of time (to delete and recreate) needs to be
done every weekend in order to just about be within the limits. 5 minutes isn't
much to 'pay' for the use of the service but if it isn't done then you might
find you have run out hours for the month!

Overall I would consider using Railway for future prototype hosting due to its
ease of use and now I understand the limitations.

### Render

Render is very easy to
[get started](https://render.com/docs/deploy-node-express-app) with due to the
[GitHub app](https://render.com/docs/github) integration.

When setting the service up, both the `build` and `start` commands will need to
be entered (`npm install && npm run build` and `npm run start`
respectively, at the time of writing). The interface also provides the ability
to enter the env vars. Differing from Railway, Render only requires the
`PASSWORD` to be set as `NODE_ENV` is set to `production`
[by default](https://render.com/docs/environment-variables#node) - a nice touch
as this also means the site doesn't work rather than being accessible on first
deployment.

Once the service was configured it seemed to take a bit longer to startup and
get running than the Railway service.

I think the main benefit of Render over Railway is the 750 hours the
[Free Plan](https://render.com/docs/free#free-web-services) provides (it can be
on all of the time). There are some limitations but they shouldn't be
a problem for the typical use cases a prototype fulfills i.e. demos and user
research. The main thing to be aware of is the service being 'spun down' after
15 minutes of activity. If that was a major concern I'm sure setting up an
uptime status checker such as [UptimeRobot](https://uptimerobot.com/pricing/)
or [statuscake](https://www.statuscake.com/pricing/) would prevent the site
from being spun down. If neither of those works using a Function as a
service (FaaS) provider such as [AWS Lambda](https://aws.amazon.com/lambda/) or
[Azure Functions](https://azure.microsoft.com/en-gb/products/functions/#overview)
with their healthy free quotas could be used to request the site on a regular
schedule!

## Conclusion

The next prototype I need to host I would choose Render over Railway, mainly
because of the 750 hours. However, it also feels more mature in terms of
documentation, configurability and services offered.
