---
title: "Revolutionising Human-AI Interaction"
date: 2025-05-01
categories: 
  - "prompting"
tags: 
  - "artificial-intelligence"
  - "co-creation"
  - "hci"
  - "prompt-engineering"
  - "ui-design"
coverImage: "researchgraph.org_wp-admin_post.php_post1816actioneditHighRes-1-1.png"
---

## The Promise and Challenges of Prompting in Creative Applications

_This article is based on the paper [**"_**How to Prompt? Opportunities and Challenges of Zero- and Few-Shot Learning for Human-AI Interaction in Creative Applications of Generative Models**_"**](https://arxiv.org/abs/2209.01390) by Hai Dang and others._

![](images/researchgraph.org_wp-admin_post.php_post1816actioneditHighRes-1-1015x1024.png)

_Created using DALL.E on 4 March 202_5

## Author

- Aditya Arora (**ORCID:** [0009-0006-5800-1198](https://orcid.org/0009-0006-5800-1198))

## Introduction

This article provides a comprehensive summary of the research paper ["_**How to Prompt? Opportunities and Challenges of Zero- and Few-Shot Learning for Human-AI Interaction in Creative Applications of Generative Models**_"](https://arxiv.org/abs/2209.01390), which explores a critical aspect of modern digital content creation: how users interact with and control advanced generative AI systems.

The research examines the emerging field of prompting - a method that allows users to guide AI models through natural language instructions. As deep generative AI systems continue to advance, producing sophisticated outputs across multiple media formats including images, text, and music, understanding how to effectively communicate with these systems becomes increasingly important.

The paper delves into the concept of prompting, which offers a user-friendly approach to interacting with AI. By using natural language instructions, users can direct AI systems without requiring extensive technical knowledge. These prompts can vary in complexity:

- Zero-shot learning: Providing instructions without any examples

- One-shot learning: Including a single example to guide the AI

- Few-shot learning: Offering multiple examples to refine the AI's understanding

For instance, a simple translation prompt might be: "Translate the following sentence into German: Good morning, how are you doing?"

While prompt engineering has gained significant research interest and generated numerous informal best practices, the paper identifies a crucial gap in understanding how to design user interfaces that make prompting more systematic and accessible. By approaching prompting from a Human-Computer Interaction (HCI) perspective, the research aims to provide insights that can help developers and designers create more effective interfaces bridging advanced AI capabilities with user needs.

The subsequent sections will explore the key opportunities and challenges in prompt-based interactions, particularly in creative applications, and present four critical design principles for developing more intuitive prompting interfaces.

## Key Opportunities

Through long brainstorming sessions with five HCI researchers, they identified the below key opportunities:

1. **Programming Creative Tools Without Code:** AI prompting systems enable users to create custom functionality without technical expertise. Users can define specific tasks through natural language prompts and save these as reusable tools. For example, a writer might create and save prompts that:
    - Convert technical text into simpler language
    
    - Transform article outlines into full drafts
    
    - Check text for consistency in tone
    
    - Generate different versions of headlines

3. **Expanding Creative Capabilities:** Prompting allows users to work with abstract or complex creative concepts that would be difficult to achieve through traditional software interfaces. For example:
    - Creative work can be translated between different formats (like turning a novel into a screenplay)
    
    - Content can be modified based on high-level directions (such as "make this more formal" or "adapt this for a younger audience")
    
    - Users can describe desired writing styles or moods in natural language. (Like rewrite your email in the style of Shakespeare)

5. **Dynamic Inspiration and Feedback:** Prompting can help overcome creative blocks by generating content when needed. More importantly, they enable interactive feedback - users can prompt the AI to evaluate their work from specific perspectives (e.g., "What would Shakespeare write here?"). The technology also supports rapid iteration, allowing users to explore multiple variations of their work based on different examples or high-level directions such as keywords and styles. For example, a marketing professional could generate five different versions of an advertisement and then mix and match the best parts of each. This creates a dynamic environment where AI assists both in generating new content and refining existing work.

## Understanding Prompt Crafting

Creating effective prompts is an emerging art form that goes beyond simple instruction-giving. While many users approach prompting through experimentation, there are strategic approaches to improve communication with AI systems.

### **Core Principles of Effective Prompt Design**

1. **Contextual Precision**
    - Establish a clear starting point for the AI
    
    - Define the desired perspective or role
    
    - Outline specific expectations for the output

3. **Structured Complexity**
    - Begin with straightforward instructions
    
    - Progressively introduce nuanced requirements
    
    - Deconstruct complex tasks into manageable components

5. **Strategic Communication**
    - Carefully consider word placement and sequence
    
    - Provide explicit guidance on desired outcomes
    
    - Use clear, unambiguous language

## Key Challenges

While these possibilities are exciting, it's a bit like having a powerful new tool that we're still learning how to use best. The research paper lists several significant challenges that need to be addressed for effective implementation of prompting interfaces:

1. **Trial and Error Process:** Currently, creating effective prompts remains largely experimental. Despite the availability of best practices shared in informal resources and emerging research in prompt engineering, users lack guidance. Word order optimisation, which involves carefully arranging words in a prompt to improve AI responses (like putting important terms first), has shown promise in research. Similarly, prompt elaboration helps by having the AI system "think aloud" through complex problems, breaking them down into smaller steps just as humans do when problem-solving. While these and other techniques exist, few of these strategies have been translated into user-friendly interfaces for non-technical users. The need for more structured approaches to prompt creation is evident, particularly for complex tasks that might benefit from breaking down into smaller, more manageable prompts

3. **Interface Design Complexities:** Representing and organizing prompts within user interfaces presents unique challenges:

- How to effectively display and organize custom prompt-based tools in the interface

- Making prompt functionality easily discoverable and memorable without requiring users to reread the underlying prompts

- Integrating images and tacit knowledge into primarily text-based prompting systems

Additionally, creative work requires multiple iterations and requires exploring different outcomes. It is a challenge how interfaces would support this. Moreover, if a prompt has to follow some rules or structure, it defeats its advantage of using natural language.

3. **Technical and Practical Limitations:**

- Large models may have processing delays, which can disrupt creative flow and limit rapid iteration. Additionally, high computational requirements may restrict access to these tools. Also, Prompt effectiveness often varies between different AI models, potentially creating dependency on specific systems, where a user may be required to continue using one model to obtain better performance.

- Content generated through prompting may reflect existing biases in language models.

## Design Goals for Effective Prompting Interfaces

The research proposes four key design goals for creating effective prompting interfaces, particularly in creative applications. Here's how these interfaces should be developed:

1. **Supporting Prompt Formulation**: The first priority in designing prompt interfaces is making it simple and quick for users to create effective prompts. This can be achieved in two ways:
    1. The first approach uses automatic parsing - the system analyses what the user types and converts it into a structured prompt automatically. Users can then fine-tune their prompt using familiar interface elements like dropdown menus. While this makes prompt creation easier, it may be limited by what the system can recognise.
    
    3. The second approach gives users more direct control. Instead of automatic parsing, users build their prompts by selecting from pre-tested prompt components.

![](images/fig%201.jpg)

**Fig. 1** Automatic input parse and create prompt

In the above GUI, the system automatically parses the user's input written in natural language and detects the task and its parameters, which can be edited directly. Then, the text prompt is created for the AI model.

2. **Supporting Users in Combining Prompts:**

The ability to combine multiple prompts effectively is a crucial feature for creative work. In creative writing, for example, this allows writers to explore different possible storylines simultaneously. Here's how it works:

A writer starts with a single prompt that generates several story beginnings. They can then review these different versions and pick which ones they want to develop further. The chosen stories become starting points for new prompts, creating a tree of possibilities.

![](images/fig%202.jpg)

**Fig 2.** Users start with a prompt, and the interface generates multiple possible outputs. Users can select some of the responses, which can be used as context for the next prompt(s), creating a tree.  
next prompt(s), creating a tree.

3. **Representing Prompts in User Interfaces**

The visual presentation of prompts in the interface is crucial for a smooth user experience. There are two main approaches to this challenge:

In the first approach, a prompt can be represented by an icon in the toolbar, similar to how bold or italics are shown in word processors. When applied to text, the prompt's effects are shown through highlights or popups, making it clear which parts of the text have been AI-assisted.

The second approach splits the screen into two views: a prompt section and a text section. This works like having two connected documents side by side. In the prompt section, users can organize and edit their prompts. The text section shows the results and allows for quick edits. This clean separation makes it easier to manage both prompts and their generated content.

![](images/fig%203.jpg)

**Fig 3.** The Interface is split between two views, prompt and text view. User can switch between editorial and evaluative tasks

4. **Supporting Users in Applying Prompts**

Beyond creating prompts, we need to think about how users will actually use them within familiar interfaces.

One effective approach treats prompts like familiar text editing tools. Users can save their favourite prompts in a toolbar, each with its own icon or symbol. To use a prompt, they simply select some text and click the prompt's icon. The system then shows the AI-generated result in a popup window.

The design also needs to handle AI processing delays gracefully. Instead of forcing users to wait, the interface can let them continue working on other parts of their text while the AI generates content. For instance, if a writer gets stuck on one paragraph, they can mark it for AI assistance and move on to writing the next section. When the AI finishes, it notifies the writer, who can then review and edit the generated text.

![](images/Text%20Prompt.png)

**Fig 4.** This interface enables users to write and save prompts as an icon in a toolbar, which can be applied to selected text by clicking the icon.

## Conclusion

Prompting marks an innovative shift in human-AI interaction, particularly for creative tasks. It transforms AI capabilities by enabling users without technical expertise to create custom tools and direct AI systems through natural language. More than just making AI accessible, this approach allows users to develop their creative skills through experimentation while expanding the possibilities of what they can create.

However, realizing this potential requires well-designed interfaces that address the challenges discussed. The design principles presented here - focusing on prompt formulation, combination, application, and representation - offer a foundation for future development. As the field evolves, continued research at the intersection of HCI and AI will be crucial for making AI-assisted creativity more effective and accessible to all users.

## References

Dang, H., Mecke, L., Lehmann, F., Goller, S., & Buschek, D. (2022). _How to Prompt? Opportunities and Challenges of Zero- and Few-Shot Learning for Human-AI Interaction in Creative Applications of Generative Models._ CHI’22 Workshops.
