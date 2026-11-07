# Prompts Used to Build the Skill

## Step 1: Initial Prompting
"I want to create an AI viva examiner skill. When I type /viva with my notes, it should ask me 5 questions one by one, wait for my response, judge my answers, and score me at the end."

## Step 2: Edge-case Refinement
"Ensure that the AI never outputs all 5 questions at once. It must strictly wait for user input after each question and provide constructive feedback before asking the next."

## Step 3: Packaging
"Convert this behavior into a standardized Markdown instruction file and a skill manifest JSON."