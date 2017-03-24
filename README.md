# Entities

- Person
- Post
- Room
- Membership (joins person to room)
- Invitation (id, token, email, room_id)
- Infraction (id, label)
- InfractionEvent (infraction_id, post_id, person_id)
- InfractionRating (infraction_id, person_id, rating 0-5)
- Emote (id, label, code)
- EmoteEvent (emote_id, person_id, post_id)

# API Endpoints

## (REMOVE) `/register`

# `/auth/validate` POST
  
in: invitation token

out: validity flag (0 = no user, 1 = user exists, http code 404 bad code)
 
- validate Invitation (valid / invalid / no user response) (200 vs 404)

# `/auth/setup` POST

when: validate returns no user

in: invitation token, handle

out: auth token

- validate Invitation
    - look up token
    - create person
    - create auth token
    - join person to room

# `/auth/join` POST

when: validate returns valid

in: invitation token

- validate Invitation
    - look up token
    - look up person
    - join person to room

# `/metadata`

in: auth

out: available emotes, available rooms

# `/room/:room_id` GET

in: auth, room_id

out: posts

    {
        id: 0,
        body: "Hey folks!",
        handle: "freddie",
        emotes: [
            { id, quantity },
            { id, quantity }
        ],
        infractions: [
            { id, quantity },
            { id, quantity }
        ]
    }

# `/room/:room_id/post` POST

in: auth, body, room_id

- validate auth, room_id membership
    - create post

# `/room/:room_id/post/:post_id/emote` POST

in: auth, room_id, emote_id, post_id

- each emote_id can be registered only once for a given person / post

# `/room/:room_id/post/:post_id/emote` DELETE

in: auth, room_id, post_id, emote_id

# `/room/:room_id/post/:post_id/infraction` POST

in: auth, room_id, post_id, infraction id

- each infraction id can be registered only once for a given person / post

# `/room/:room_id/post/:post_id/infraction` DELETE

in: auth, room_id, post_id, infraction id
