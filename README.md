# Entities

- Person
- Post
- Room
- Membership (joins person to room)
- Invitation (id, token, email)
- Infraction (id, label)
- InfractionEvent (infraction_id, post_id, person_id)
- InfractionRating (infraction_id, person_id, rating 0-5)
- Emote (id, label, code)
- EmoteEvent (emote_id, person_id, post_id)

# API Endpoints

## (REMOVE) `/register`

# `/auth/validate`
 
in: invitation token
 
- validate Invitation
    - look up token
    - user exists with email?
        - no: collect handle (?!), create person, create auth token
        - yes: 



