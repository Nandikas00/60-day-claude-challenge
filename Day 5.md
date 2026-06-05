These were the two prompts I gave to claude and following outputs were given by ai:

# PROMPT A (WITHOUT CONTEXT)

Create a 30-day learning roadmap.

Include:
- Weekly milestones
- Daily tasks
- Resources
- Projects
- Final outcome

Make it practical and beginner-friendly.

OUTPUT:
<img width="1915" height="901" alt="Screenshot (104)" src="https://github.com/user-attachments/assets/7793a8d9-5123-4f2b-9bd6-dfc04c05a79a" />

# PROMPT B (WITH CONTEXT)
Continue without answerinCreate a 30-day learning roadmap.

Context:
- Current Situation: Looking for job
- Current Skills: Python , excel, power bi, mysql, c/c++
- Goal: To improve my data analytics skills 
- Available Time: 1 hr /day
- Experience Level: Beginner
- Preferred Learning Style: Reading

Include:
- Weekly milestones
- Daily tasks
- Resources
- Projects
- Final outcome

Make it practical and beginner-friendly.

Compare both outputs and identify:
1. Which roadmap feels more personalized?
2. Which roadmap would you actually follow?
3. What role did context play in improving the result?

OUTPUT :
<img width="1915" height="901" alt="Screenshot (104)" src="https://github.com/user-attachments/assets/fa6eb099-9675-40d3-8dd9-f6d060c69f2c" />


## Key Learnings from Prompt Engineering Experiment

1. Context Creates Better Personalization
The roadmap generated using normal prompting produced a generic Python learning plan focused on beginner concepts such as variables, loops, functions, lists, and dictionaries.
In contrast, the roadmap generated using context prompting leveraged my existing skills in Python, Excel, Power BI, and MySQL and created a specialized Data Analytics roadmap. This demonstrated how providing background information helps AI generate content that is more aligned with individual goals and current skill levels.
2. AI Shifts from Generic to Goal-Oriented Planning
Without context, the AI assumed a beginner learning path. With context, it identified my objective as becoming job-ready in Data Analytics and focused on advanced SQL concepts such as:
Joins
CTEs (Common Table Expressions)
Window Functions
Data Cleaning
Analytical Query Writing
This showed that context enables AI to optimize recommendations toward a specific career outcome rather than providing broad educational content.
3. Project Recommendations Become More Relevant
The generic roadmap suggested a Number Guessing Game project to practice programming fundamentals.
The context-aware roadmap recommended an E-commerce Sales Analysis project using SQL, which directly reflects real-world data analyst responsibilities and portfolio-building needs.
4. Better Resource Selection
The normal prompt recommended general Python learning resources, while the contextual prompt recommended resources specifically useful for analytical SQL learning and interview preparation.
This highlighted how context improves resource relevance and learning efficiency.
5. Reduced Learning Redundancy
Since the contextual prompt included information about existing skills, the AI avoided repeating topics I already knew and instead focused on skill gaps. This makes learning plans more efficient and time-effective.

💡 Biggest Insight
The quality of AI-generated output depends heavily on the quality of context provided.
The experiment showed that prompt engineering is not only about asking the right question but also about supplying the right background information. Context transformed a generic learning roadmap into a personalized, career-focused action plan aligned with my existing skills and professional goals.

🎯 Conclusion
This comparison demonstrated that context prompting significantly improves relevance, personalization, project quality, and career alignment, making it a powerful technique for generating practical and actionable AI outputs.
