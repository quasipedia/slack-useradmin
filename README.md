# Slack-UserAdmin

**A tool to streamline user management on Slack**

Oftentimes, people within an organisation need or must be part of Slack private
groups or public channels based on their roles (for example they may need to be
part of their team's private group, but also be part of several cross-team
channels based on their skills and functions).

Setting up a large organisation on Slack can therefore be a long and tiresome
activity of creating channels and groups and inviting people to them.

Additionally, people may change roles or functions along the way, new people
may join the organisation, etc... and keeping track of all the changes can be
time consuming and prone to errors.

Slack-UserAdmin is a tool to streamline the management of users on Slack.
And provides facilities for:

  - Positively **link an organisation e-mail address with a Slack username.**
  - **Associate descriptors (tags) to people** so as to specify information
    such as function, title, location...
  - **Use tags to automate Slack tasks** (for example: "Create a new private
    group `#javascript` and invite everybody who has been tagged
    `frontend-developer` to it").
  - **Automatically keep in sync** chages between a person's descriptors and
    their membership in channels/groups.

# Naming conventions

  - **user** - Any person in the organisation that ought to have a Slack
    account (so: the _user_ may or may not have an accoun on Slack yet).
    _Users_ are identified by their e-mail addresses.
  - **maverik** - Any person who has a Slack account but whose slack identity
    hasn't been associated [yet] to a _user_ via Slack-UserAdmin. _Maveriks_
    are identified by their Slack user name.
  - **slackizen** - Any person who has a Slack account and whose slack identity
    has been associated to a _user_ via Slack-UserAdmin. _Slackizens_ are
    identified by their Slack user name.
  - **tag** - _Tags_ are associated to _slackizens_.  They don't have any
    implicit semantics, so they can be used to denote anything: team
    affiliation, job titles, location, competences, gender....
  - **roles** - A _role_ is associated to _slackizens_.  A role define the set
    of permissions a _slackizen_ is given.  Roles can be only one of the
    following:
    1. **admin** - _Admins_ have access to all the features of Slack-Useradmin.
    2. **dominus** - _Domini_ administrate all _slackizens_ whose e-mail has
       the same domain.
    3. **member** - _Members_ are all _slackizens_ who don't enjoy any
       particular permission.

# Example workflow

1. An international company opens a Slack account, registering all their
   thousands of employees with their `<company>.com` e-mails.  At this point
   every person on Slack is a _maverik_.
2. The _admin_ appoints a _dominus_ for each national office (e.g.:
   `<company>.se`, `<company>.de`, `<company>.nz`)
3. Each _dominus_ associates _maveriks_ to their national _users_, thus
   converting them into _slackizens_.
4. Each _dominus_ tags the _slackizens_ under their control appropriately (this
   may means different things for different countries).
5. Each _dominus_ associate tags (or combinations of them) to channels/groups.
6. All channels and/or groups are automatically created, and the correct
   _slackizens_ are automatically invited to them.

# Commands

The following is the complete list of commands available in Slack-Useradmin.

## send-token E-MAIL ...

[admin, dominus]

    /xxx send-token alpha@example.com bravo@example.com charlie@foobar.nz

Send a unique, distinct token to each of the mail adresses given as parameters.
The token is later to be used with the `i-am` command.

## i-am TOKEN

[member]

    /xxx i-am 7f0aacbd-d220-4450-a9c0-4a23d4f7ec26

The _maverik_ issuing this command will associate their account to the _user_
whose token has been generated for.  If the command succeeds, the _maverik_ is
now a _slackizen_.

## they-are SLACK-USERNAME USER-EMAIL

[admin, dominus]

    /xxx they-are @goldenunicorn foo.bar@example.com

Has the same effect of `i-am`, but does not require sending tokens nor any
action from the _maverik_'s side (requires you to know who the hell is
@goldenunicorn, though!)

## me

[admin, dominus, member]

    /xxx me

Return informations on associated e-mail[s] for the slackizen, their tags and
participation in groups/channels.

## tag USER-EMAIL ±TAG ...

[admin, dominus]

    /xxx foo.bar@example.com +dev +front-end +junior
    /xxx spam@example.com -junior +senior
