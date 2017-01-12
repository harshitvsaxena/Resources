<a id="top"></a>

# Mattermost VS Rocket.Chat

## Mattermost Features:

- Search (Using #hashtags) - serach is pretty awesome.
- Highly customizable (Design wise)
- Can integrate in mobile apps.
- Rich text formatting.
- Attach any kind of file.
- Docker image available: https://hub.docker.com/r/jasl8r/mattermost/
- Good documentation.
- Video/Audio Conference not available (They are working on it - will be available in future)

## Rocket.Chat Features:

- Highly customizable.
- Attach any kind of file.
- Rich text formatting available.
- Docker image available.
- Okay documentation but not as good as mattermost.
- More importance to customer care type.
- Video/Audio conference available.
- File sharing available.
- Can integrate in all kind of devices.
- Search ability available.

---

## Case Studies: 

### Case 1: How much work to do to get the database going and linking with the source code of both of these chat services.

#### Mattermost

Database connectivity is pretty straight forward. Link: https://hub.docker.com/r/jasl8r/mattermost/#database

But the one thing they have mentioned is for file sharing the mattermost stores data in the file system for features like file upload and avatars. To avoid losing this data you should mount a volume at,

- `/opt/mattermost/data`

The documentation for that is also available at: https://hub.docker.com/r/jasl8r/mattermost/#data-store

I don't think it should take much time, probably not more than 1 or 2 hours.

#### Rocket.Chat

Rocket.chat does not have MySQL support they mainly support MongoDB although they are working on providing support for PostgreSQL.

Setup for MongoDB with Rocket.Chat is also pretty straight forward. Here is the link: 

- For Aliyun(Alibaba Cloud): https://rocket.chat/docs/installation/paas-deployments/aliyun/#start-the-mongodb-database
- For AWS: https://rocket.chat/docs/installation/paas-deployments/aws/#7-set-up-docker-containers

I would say the setup of Rocket.Chat is slightly more complex than Mattermost, mostly on AWS.

---

### Case 2: Ability to chat.

Both are having same kind of UI but are highly customizable and I would say they are both equally good in ability to chat.

---

### Case 3: Ability to create groups only by admins. Users should only be able to join and type their messages and see them.

#### Mattermost

Yes, Mattermost allows for this ability, look at this link: https://mattermost.uservoice.com/forums/306457-general/suggestions/11205624-only-admin-or-manager-should-be-able-to-create-cha

#### Rocket.Chat

From the links below it seems they are still developing this feature

- https://github.com/RocketChat/Rocket.Chat/issues/658
- https://github.com/RocketChat/Rocket.Chat/issues/630

---

### Case 4: Send smileys, pics, videos, audios.

#### Mattermost

Yes, it is available. Demo is available at this link: https://gitlab.mattermost.com/signup_user_complete/

#### Rocket.Chat

Yes, it is available. Demo at this link: https://demo.rocket.chat/

---

### Case 4: One-to-one chat conversation

- Share screen when on one-one chat conversation
- Video recording and/or sharing, audio recording and sharing

#### Mattermost

Yes, one-to-one, video/audio sharing/recording is available but screen-share and video/audio conference is not available as referred from links below:

- https://mattermost.uservoice.com/forums/306457-general/suggestions/10625343-video-audio-conference-feature
- https://mattermost.atlassian.net/browse/PLT-2048

#### Rocket.Chat

Yes, everything asked in this case are available.

---

### Case 5: Ability to select only required features, for example, if in one page we want to have only video sharing capability, but not anything else, can we do it? Also remember that, in another page, we need to use same application with different features.

I don't know about this, but as far as I have seen their documentations, it seems that yes it is possible in both.

---

Disclaimer: Above information is provided using many resources, and correctness of every information provided can not be guaranteed.

[Top](#top)

---

## The End
