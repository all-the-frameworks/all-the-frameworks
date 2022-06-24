# All The Frameworks

This repo is a container for things like the Project Manager design docs,
shared assets, and other such things. Most of that lives in the wiki attached
to this project.

## Project Manager

Project Manager is an example application designed to be broadly representative
of the sort of application a SaaS startup is likely to produce, providing a
known set of functionality that can be reproduced across many different
frameworks.

At it's core Project Manager is a basic tool for tracking progress on work in a
small company. Many people can create projects, with tasks within them, and
discuss the development of those tasks.

### Features

* CRUD for projects, which are just a container for a number of tasks
* CRUD for tasks, which have a state tracked against them
* Activity logs for tasks
* File attachments
* Email notification of task updates
* Multiple users
* Multiple organisations, with a user being able to join one or more organisations
* Stripe payments and basic billing management

### Organisations

An organisation groups together a set of users, any projects they're collaborating
on, and billing for all of the above. For billing purposes an organisation has
a set of entitlements attached to it which describe what functionality they're
allowed to use.

### Users

A user represents a single person who can access Project Manager. They can be
associated with multiple organisations, and given different privileges for each
organisation they are a member of.

All authentication is managed by [Clerk](https://clerk.dev) because nobody
should be doing their own auth these days unless its absolutely core to their
business.

### Projects & Tasks

People would be coming to Project Manager to work on projects, so we need some
support for them. A project contains a bunch of tasks, and a description. When
you're done with one you can archive a project which makes it read only.

Depending on what plan organisations have subscribed to they'll be able to have
a number of active projects at the same time.

Within a project are any number of tasks, which represent a piece of work to be
done. They carry with them a state, a description, an owner, and any number of
people who are watching the task. People who are watching get notified of updates.

#### Activity Logs

The activity log for a task records what has been happening, such as state changes
and also allows people to comment on how progress is going. They work like comment
threads do in every other application ever.

Anyone watching a task will get notified when new items are added to the activity
log.

### Activity Updates

(Mostly so that scheduled jobs happen) people can opt in to get an overview email
of progress for a project each day.