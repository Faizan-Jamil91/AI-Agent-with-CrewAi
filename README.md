AI-Driven Content Creation System
This project demonstrates the use of AI agents to automate the research and writing process for creating engaging and factually accurate articles using CrewAI.

Project Overview
The project consists of three AI agents, each with distinct roles and responsibilities:

Content Planner Agent: Develops a comprehensive content plan.
Content Writer Agent: Crafts a compelling blog post based on the content plan.
Editor Agent: Reviews and finalizes the blog post for publication.
Project Workflow
Planning: The Content Planner Agent collects information, prioritizes trends, identifies the target audience, and creates a detailed content outline with SEO keywords.
Writing: The Content Writer Agent uses the content plan to write a well-structured blog post, incorporating SEO keywords and ensuring grammatical accuracy.
Editing: The Editor Agent reviews the blog post for alignment with journalistic best practices and the organization's voice, ensuring the final output is ready for publication.
Installation
To set up the project, you need to install the required packages. You can do this using pip:

bash
Copy code
pip install crewai==0.28.8 crewai_tools==0.1.6
Usage
Here's how you can use the system to create a blog post:

Define Agents and Tasks:
python
Copy code
from crewai import Agent, Task, Crew

planner = Agent(
    role="Content Planner",
    goal="Plan engaging and factually accurate content on {topic}",
    backstory="You're working on planning a blog article about the topic: {topic}.",
    allow_delegation=False,
    verbose=True,
    llm=llm
)

writer = Agent(
    role="Content Writer",
    goal="Write insightful and factually accurate opinion piece about the topic: {topic}",
    backstory="You're working on writing a new opinion piece about the topic: {topic}.",
    allow_delegation=False,
    verbose=True,
    llm=llm
)

editor = Agent(
    role="Editor",
    goal="Edit a given blog post to align with the writing style of the organization.",
    backstory="You are an editor who receives a blog post from the Content Writer.",
    allow_delegation=False,
    verbose=True,
    llm=llm
)

plan = Task(
    description=(
        "1. Prioritize the latest trends, key players, and noteworthy news on {topic}.\n"
        "2. Identify the target audience, considering their interests and pain points.\n"
        "3. Develop a detailed content outline including an introduction, key points, and a call to action.\n"
        "4. Include SEO keywords and relevant data or sources."
    ),
    expected_output="A comprehensive content plan document with an outline, audience analysis, SEO keywords, and resources.",
    agent=planner,
)

write = Task(
    description=(
        "1. Use the content plan to craft a compelling blog post on {topic}.\n"
        "2. Incorporate SEO keywords naturally.\n"
        "3. Sections/Subtitles are properly named in an engaging manner.\n"
        "4. Ensure the post is structured with an engaging introduction, insightful body, and a summarizing conclusion.\n"
        "5. Proofread for grammatical errors and alignment with the brand's voice.\n"
    ),
    expected_output="A well-written blog post in markdown format, ready for publication, each section should have 2 or 3 paragraphs.",
    agent=writer,
)

edit = Task(
    description=("Proofread the given blog post for grammatical errors and alignment with the brand's voice."),
    expected_output="A well-written blog post in markdown format, ready for publication, each section should have 2 or 3 paragraphs.",
    agent=editor
)

crew = Crew(
    agents=[planner, writer, editor],
    tasks=[plan, write, edit],
    verbose=2
)
Run the Tasks:
Execute the tasks to create the blog post. Here’s an example of how to initiate the tasks:

python
Copy code
crew.run(topic="Latest Trends in AI")
Output
The system will generate a well-written blog post in markdown format, ready for publication. Each section will have 2 or 3 paragraphs, ensuring the content is engaging and well-structured.

Benefits
Automation: Streamlines the entire content creation process.
Efficiency: Saves time and resources by delegating tasks to specialized agents.
Quality: Maintains high standards of content through rigorous planning, writing, and editing.
Contributing
If you wish to contribute to this project, please fork the repository and submit a pull request. For major changes, please open an issue first to discuss what you would like to change.

License
This project is licensed under the MIT License.
