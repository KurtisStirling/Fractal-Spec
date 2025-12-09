answer: I moved the lint file into a new @future-enhancments/ folder. Please do you recommendations re; navigation examples. For spec template, we need to make it smaller 
so easier to use for humans on small use cases (and can make sure the verify-requirements and verify-design commands explicity say that more fields can be added e.g.
 (some of the default feilds we removed from the template). Once the template is smaller, i wonder if we should put it inside the guide so we just have a single 
master file that explains/provides everything?

answer: i thought of a good rule for when to plan: anything that you think would take 25% of your tokens in one go to do properly (50,000 tokens or more)

answer: can we add some more "progressive discloser" to the new convesation startup read flow (claude will point to this framework as a must-read when doing any work in the repo) then it (should) read just the llm section of the framework guide (should stop where it says dont read paste here - do we need to test this?). The goal is to make the initial startup new convo must-read material for functional specs use in the repo, it needs to tell it all in needs to know in minimal tokens possible. I think some branching progressive/selective disclosure would help this. 

task: do any prep needed to package this for release - end product needs to be extremely easy to add to new repos

task: do a final review and "make it more terse" run

task: release to github