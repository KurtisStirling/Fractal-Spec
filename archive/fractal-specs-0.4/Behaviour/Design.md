# Behaviour / Design

- Lifecycle: demand (Requirements) → planning (Plan) → supply update (Design) → promotion/cleanup.  
- Local reasoning: each subject owns its own lifecycle; partial updates allowed without global rewrites.  
- Roll-up: completion rolls up from child subjects to parents via updated Design/Requirements, not by copying plans upward.  
- Done: work is done when implementation ships and Design/Requirements reflect the as-built system; plans/research are then cleaned or archived.  
- Demonstrated in this meta-model and the RPI example under `work/`.
