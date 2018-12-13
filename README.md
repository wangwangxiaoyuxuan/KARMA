# KARMA -- a Consequence Focused Narrative Generating System

Author: James Wang
Date: 13th of December, 2018

In this README there is:
1. Overview and Introduction
2. Why Focus on Consequences
3. System Architecture
4. Computational Creativity Evaluation
5. KARMA’s Effect on Me

## Overview and Introduction
The KARMA project, standing for Karmic Aspect Revolving Media Arranger, is a system that in which I attempt to generate narratives where actions have causes and consequences. In the impressive existing works on computational narrative generation, there are already systems that seem to keep track of its own story’s events and show their continuing effect. Two of the best examples I found are from Botnik Studios and Pablo Gervás. Botnik’s *Harry Potter and the Portrait of what Looked Like a Large Pile of Ash* demonstrates a system that can narratively follow the effects of one action for a couple of lines via text predictions. The PropperWryter system modified from Gervás used for *Beyond the Fence* generates coherent plots with existing story schemas and a selection of actions available to the characters. While the depth and polish of both Botnik and PropperWryter and their products are much beyond the current KARMA system, from what I know of those systems and what I plan for mine, KARMA explores a method of narrative generation that should more clearly and intentionally model character interactions’ causes and effects.

## Why Focus on Consequences
Before proceeding to describe KARMA, I want to show the purpose of consequence-focused systems such as it. Consequence focused narrative systems interest me because stories where characters commit actions for reasons and the actions cause sprawling effects are more interesting to think about and re-read. In other words, engaging stories have characters who make sympathizable choices that impact their world.

I borrow my point about the importance of consequential actions from Anton Chekhov, a great writer and one of the fathers of early theatre modernism. He maintains in a letter to his friend that it is important to “[r]emove everything that has no relevance to the story. If you say in the first chapter that there is a rifle hanging on the wall, in the second or third chapter it absolutely must go off. If it's not going to be fired, it shouldn't be hanging there.” This is now known as Chekhov’s Gun. Only add an element to a story if that element will have an effect. Or: every action must have a consequence.

Besides having consequences, actions must also have reasons. This I gather from Dan Harmon, a contemporary writer and creator for popular TV shows such as *Community*, *HarmonQuest*, and *Rick and Morty*. For example, often in his animated shows, he sets up a scene that one expects to cumulate in a dazzlingly heroic deed, then, he subverts this expectation by writing the character to do something grotesquely unheroic, and finally, he gives that character an easily sympathizable reason for their failure. While the expectation and subversion of heroism generate anticipation and intrigue, it is the character’s explanation for the subversion relates the character to the audience and makes for a compelling moment. By giving well-designed motives to well-placed actions, Harmon humanizes his characters and crafts compelling moments.

Anyways, I am not alone in thinking that an engaging story’s characters act from an understandable cause to an understandable effect. For being such an important part of writing, it is unfair that consequential storytelling is underdeveloped in the computational creativity research world. The ideological purpose behind consequence-focused systems like KARMA is to consider actions’ causes and effects more closely to generate better stories.

## System Architecture
### Ideal System Architecture for KARMA
In this section, I will describe the system architecture for the current ideal version of KARMA through its several processes: History generation, History to Script translation, Script evaluation, and the Improvement Engine.

#### History generation
History generation is the initial process in KARMA’s generation of a consequence-focused narrative that cumulates in the creation of a “History,” which is a list of sequenced actions detailed by their doers, recipients, causes, and effects. In other words, a plot map. An entry in a rudimentary History might look like “382. Action: murder. Doer: Bongo. Recipient: Ipsic. Cause: Bongo was poor, jealous, hateful, weak, opportunistic, and Ipsic was rich, contemptuous, arrogant, strong, distracted. Effect: Bongo is poor, jealous, hateful, weak, opportunistic, tired, insecure and Ipsic is rich, contemptuous, arrogant, strong, distracted, surprised, dead.” To have material from which to draw actions and their causes and effects, this section uses a database that curates examples of action causes and effects. This includes testimonies, psychological studies, news and journal articles, fiction, and any text that describes decisions’ motives or actions’ consequences, physical or psychological. From this database, the Cause and Effect interpreter creates generalizations for actions and associates certain character qualities with each of them as causes or effects. Finally, with computationally understandable sets of actions qualities, the History Generator writes a long history by creating characters with given qualities and following their trail of actions and effects.

#### History to Script translation
Given the History object from the previous process, the next step in KARMA is to make a Script out of the plot map. For this task, the system will consult a database of natural English language that should contain everything from film dialogue to salesman speeches. The purpose of this database is to provide a thorough basis of texts and their encapsulated meanings. From this, the Natural Language Interpreter learns how to express the meaning contained in a History entry through natural language. Partially, that also requires understanding how to edit and sequence information: what to leave unmentioned, what to elaborate on, and how to order the revealing of the actions. With this knowledge, the History to Script Translator transforms the History’s cold recounting of every action to something akin to a narrative piece.

#### Script evaluation
Now comes the time to evaluate the Script. For this, KARMA consults a database of relevant literary material, the critical and public reception of each piece, and also metaliterature such as Robert McKee’s *Story: Substance, Structure, Style and the Principles of Screenwriting* and John Truby’s *The Anatomy of Story: 22 Steps to Becoming a Master Storyteller*. This section’s interpreter then judges literary pieces by their reception and generate connections relating their reception to their style and their adherence to the metaliterature guidelines. Finally, the Script Evaluator will judge the system’s own creation and releases it as an output if it scores reasonably well.

#### Improvement Engine
As the Script enters the outside world and receives evaluations from human eyes, KARMA arranges the Script and its critical and public reception into a database similar to the previous section’s database for literature and their appraisals. The content of this database provides the resources to KARMA’s Improvement Engine. Its first function is to annotate KARMA’s previously generated pieces with areas of change and sends it back through the narrative generation system to make edits. Secondly, the Improvement Engine also adjusts each of the three previous processes to learn. This circles KARMA together as a learning and knowledgeable consequence-focused narrative generation system.



### Detailed System Architecture for the History Generator
In this section, I will describe the central aspect of this project, the History Generator, starting with its inspiration and then gradually moving through its system architecture.

#### Inspiration
To George R. R. Martin I owe gratitude for the design of the History Generator portion of KARMA. Martin is another writer that demonstrates the importance of having a cause and effect for every action. In his book series, *A Song of Ice and Fire*, the literature behind the acclaimed *Game of Thrones* TV show, there is an impressive complexity in his characters. I think that, beyond drawing inspirations from “real history” to avoid writing “simple fantasy” and using “emotional truth […] to make your characters feel real,” his complex characters are products of his journey-oriented writing style. He describes himself as more of a “gardener” than an “architect” when it comes to writing. Instead of knowing “how many rooms there are going to be, how high the roof will be,” Martin prefers to “just dig a hole and plant the seed and see what comes up.” What entails are stories that faithfully follow its characters. In an interview that I can no longer locate, I seem to recall Martin saying that he just lets the characters write themselves. While this approach to writing has its deterrents (Martin also says that having to rewrite sections where the characters lead themselves into a prematurely dead end is why he writes so slowly), the result is a story where the characters feel like they belong.

#### System Architecture –– Qualities, Characters, and Actions
KARMA’s History Generator takes the same approach. After the Cause and Effect Interpreter completes its study of its database, it compiles the massive and detailed Qualities Set and Actions Set. The Qualities Set contains Quality objects that are keywords which describe a single aspect of a character. A Quality may happen to be unique to a specific character, but each Quality is representative of a state, whether it is personality, relationship, mood, or physical or ideological condition, which could apply to any character. Building on Qualities, the Actions Set contains Action objects, keywords which represent a single action with a table associated Qualities. Also build from Qualities is the Character object, which is fairly straightforward with a name, a list of Qualities, and a end condition such as death. A rudimentary example of an Action (Murder) and its associated Qualities follows:
To read the table: each cell of the pink row contains the Doer Character’s Qualities Set, each cell of the blue column contains the Recipient Character’s Qualities Set, and each orange cell contains the resultant effects on both Characters. (Note: the blank cells are only indicators for the purposes of this demonstration, as a data structure, only the colored cells exist.) At the moment, this table is incapable of producing a Murder Action with complex and relatable causes and effects. This is partially because each Character’s Qualities Set is too small, so an increase in available Qualities that would have made this table unsuitable for illustration will add complexity and nuance to the motivation. The lack of relatability, I think, is because this table does not expound on why the Characters have their current Qualities. More History is the solution since those Histories are the Actions and the backstory that created these Qualities in the first place.

#### System Architecture –– History Writing and Picking the Action
As soon as the Action Tables finish populating and the Character Generator polishes the cast, the History Writer module takes the Actions Set and Characters Set to create the narrative’s plot.

Evaluating the KARMA system with SPECS:
Active Involvement & Persistence
Dealing with Uncertainty
Consequence interpreter
Domain Competence
Depends on database interpreters
General Intellect
Generation of Results
Definitely can make something new
May have difficulty in knowing when to stop generating History
Independence and Freedom
Bound to patterns of language, format of chosen media (screenplay, play, literature, etc.). Somewhat bound to general story structures.
Can develop own style beyond pastiche when given enough human feedback and when Improvement Engine has enough training.
Intention & Emotional Involvement
Originality
Product makes sense because it’s a series of events with all explanations
Product will be surprising because of hidden qualities and unexpectable actions
Unique when it’ got all the databases and interpreters implemented
Output easily reinterpretable as long as not all cause and effect explained during history to script translation
Progression & Development
Learns after each human evaluation of generated script
Social Interaction & Communication
System easily affected by types of databases and feedback
Spontaneity/Subconscious Programming
Adding new characters during history writing and spontaneous system integration of them
Thinking and Evaluation
Evaluation of possible actions
Evaluation of end script
Have thought to back up all action choices
Value
Difficult to judge if system creates valuable artifacts until everything is fully implemented
Theoretically, should be good
Follows stylistic and linguistic constraints
Variety, Divergence, and Experimentation
Variety of characters, likely to never have the same character twice (given good consequences database and consequences interpreter)
Random choice of top likely actions and character additions cause divergence
Successful experiments pass through evaluator and become results
One problem I can see is that the characters generated with largely random background qualities may be difficult to relate to because they aren’t likely to be archetypal representations of the audience
