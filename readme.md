Proof of Puzzle Canister (Popcan!)
---

An IC native captcha-like.

- IMPETUS: Provide an open internet service that allows IC developers to easily incorporate mild anti-sybil in their applications. Many early internet computer projects struggle with bots, scripts, and highly motivated human actors that can cause damage by occupying more resources that one person should. This is a category of problem (often referred to as "Sybil attacks") that requires a spectrum of solutions to serve many contexts. This tool should provide developers with a way to slow down Sybils, which can be invaluable for mitigating time sensitive apps like a public sale of NFTs.  
- PRIMARY COMPONENTS:
    - Puzzle management:
        - Puzzles are the things you send to users to solve, which is then compared to the known solution.
        - Puzzles should probably be html. This allows for a very arbitrary execution environment, which will be valuable when iterating user interfaces.
        - There should be a system to provision/maintain a passable set set of puzzles and solutions.
    - Proof coordination:
        - A process whereby popcan, a user, and a client canister can coordinate a proof of the user's ability to solve one of our puzzles.
    - Payments:
        - I think there may be a natural way to set up payments to fund the canister, spin off a little ICP/cycles for the developer, and protect popcan itself a little bit.
- PUZZLE MANAGEMENT
    - Puzzles should be simple, easy and accessible for a person to solve, but hard for a computer. The state-of-the-art is an image data-tagging UI, but we can be simpler than that to start.
    - There must be a fairly large set of puzzle and solution pairs, which could be a fixed set or a generation method.
    - Popcan must be able to randomly select one of these sets when requested.
- PROOF COORDINATION
    - Possible Flow #1
        - Client canister generates a memo and provides this to the user agent
        - User agent submits this memo to popcan
        - Popcan returns a puzzle
        - User solves puzzle and submits solution to popcan
        - Seeing a valid solution, popcan returns a signed memo to the user agent
        - User agent submits signed memo back to the client canister
    - Possible Flow #2
        - Client canister requests a proof from popcan, with cycles / ICP in the request.
        - Popcan returns an html puzzle payload and a solution.
        - Client canister forwards the puzzle payload to user agent.
        - User agent sends solution to client canister.
        - Client canister validates solution.
    - Popcan would not prescribe any duration on the signed memo, and it would be up to the client canister how often to require proofs
    - There may be multiple valid flows for proof coordination. Identifying the best one will be an exercise.
- NOTES
    - V1 puzzles can be simple! Simply having anything in place will help slow down Sybil, especially when the service is new and it's adoption is very limited. Using html puzzles will allow easy upgrading in the future.
    - Probably easy to find some initial "clients for this project." Many projects have this problem. I would use it for my sales, maybe DSCVR or Distrikt would try it? Helpful for planning an acceptance criteria.
    - Cross subnet calls will be a sticking point.
