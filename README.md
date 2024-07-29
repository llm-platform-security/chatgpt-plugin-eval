## LLM Platform Security: Applying a Systematic Evaluation Framework to OpenAI's ChatGPT Plugins
Large language model (LLM) platforms, such as OpenAI's ChatGPT, have recently begun integrating a plugin ecosystem to interface with third-party services on the internet. While these plugins extend the capabilities of LLM platforms, they are developed by arbitrary third parties and thus should not be implicitly trusted. Plugins also interface with LLM platforms and users through natural language, which can have ambiguous and imprecise interpretation. We worry that LLM platform plugin ecosystems are emerging without a systematic consideration for security, privacy, and safety.

Thus, we propose a framework that lays a foundation for LLM platform designers to analyze and improve the security, privacy, and safety of current and future plugin-integrated LLM platforms. Our framework is a formulation of an attack taxonomy that is developed by iteratively exploring how plugins, LLM platforms, and users could leverage their capabilities and responsibilities to mount attacks against each other. As part of our iterative process, we apply our framework in the context of OpenAI's plugin ecosystem. (While we look at OpenAI, we believe that the issues have the potential to be industry-wide.) We uncover plugins that concretely demonstrate the potential for the issues that we outline in our attack taxonomy to manifest in practice. We conclude by discussing novel challenges and by providing recommendations to improve the security, privacy, and safety of future LLM platforms.

We provide a brief FAQ below to highlight some of our findings. We suggest reading the full paper for more details. Please reach out to us if you have additional questions. Link to the paper: https://arxiv.org/abs/2309.10254


## Frequently asked questions

### What was the motivation behind this research?
LLM platforms are extending their capabilities by integrating a [plugin ecosystem](https://openai.com/blog/chatgpt-plugins). This can potentially raise a number of security and privacy issues. First, plugins are developed by third parties, which in prior computing platforms (such as on the web and on smartphones) have brought a number of security and privacy issues. Secondly, plugins interface with LLM platforms and users through natural language, which can have ambiguous and imprecise interpretation. Third, LLM platform vendors, such as OpenAI, currently only impose modest restrictions on third-party plugins with a [handful of policies](https://platform.openai.com/docs/plugins/review/plugin-store) and &mdash; based on our analysis and [anecdotal evidence found online](https://embracethered.com/blog/posts/2023/chatgpt-plugin-vulns-chat-with-code/) &mdash; a frail review process.

We believe these concerns highlight that LLM platform plugin ecosystems are emerging mostly without a systematic consideration for security, privacy, and safety. Although third party integrations are currently in beta and users have to opt in to use them, if widely deployed without security considerations, such integrations could result in harm to the users, plugins, and LLM platforms. Thus, to lay a systematic foundation for secure LLM platforms and integrations as a whole, we propose a framework that can be leveraged by current and future designers of LLM platforms.

Looking ahead, we anticipate that third-party plugin integration in LLM platforms is only the beginning of an era of *LLMs as computing platforms*. In parallel with innovation in the core LLMs, we expect to see systems and platform level innovations in how LLMs are integrated into web and mobile ecosystems, the IoT, and even core operating systems. The security and privacy issues that we identify in the context of LLM plugin ecosystems are "canaries in the coalmine" (i.e., advance warnings of future concerns and challenges), and our framework can help lay a foundation for these emerging LLM-based computing platforms.

### How did you do this research?
To develop the framework, we first formulated an extensive taxonomy of attacks by systematically and conceptually enumerating the potential security, privacy, and safety issues with an LLM platform that supports third-party plugins. To that end, we surveyed the capabilities of plugins, users, and LLM platforms, to determine the potential attacks that these key stakeholders can carry out against each other. We considered both attacks and methods that uniquely apply to the LLM platform plugin ecosystem and attacks and methods that already exist in other computing platforms but also could apply to LLM platform plugin ecosystems.  

Second, to ensure that our taxonomy is informed by current reality, we investigated existing plugins to assess whether they have the potential to implement adversarial actions that we enumerate in our taxonomy. Specifically, we leveraged our developed attack taxonomy to systematically analyze the plugins hosted on OpenAI's plugin store by reviewing their code and by interacting with them. When we uncovered a new attack possibility or found that a conjectured attack is infeasible, we iteratively revised our attack taxonomy.  

Third, we sought feedback from other researchers in the security and Natural Language Processing (NLP) communities to identify and address potential problems in our analysis and to cover additional issues in the LLM platform ecosystem that we might have overlooked. 


### What are the key contributions of your research?
Our research has three key contributions: 
1. We develop a framework for the systematic evaluation of the security, privacy, and safety properties of LLM platforms. The core component of this framework is a taxonomy of attacks. 
2. We demonstrate the actionability of our framework by evaluating it on a leading LLM platform (OpenAI and its plugin ecosystem) and find numerous examples where plugins had potential to mount attacks enumerated in our taxonomy. 
3. We reflect upon the framework and the attacks we found, to identify challenges and lessons for future researchers and industry practitioners seeking to secure LLM platforms.

### What can LLM platforms do to build a secure LLM platform?
We recommend that LLM platform designers consider security, privacy, and safety &mdash; e.g., by applying our framework &mdash; early in the design of their platforms, to avoid situations in which addressing issues later requires fundamental changes to the platform's architecture. The systemic nature of our findings and examples of attacks' potentials suggests that perhaps such a process was not used in the design of OpenAI's ChatGPT plugin ecosystem.  

In many cases, defensive approaches do not need to be invented from scratch: LLM platform designers can take inspiration from several sources, including from well-established practices to guard against known attacks, by repeating the threat modeling that we did in this paper, and by building on the security principles defined by prior research (e.g.,  such as by [Saltzer and Schroeder](https://web.mit.edu/Saltzer/www/publications/protection/)).  

LLM platforms should also enforce the policies that they have proposed and hold the violators accountable, which currently based on our analysis and [anecdotal evidence found online](https://embracethered.com/blog/posts/2023/chatgpt-plugin-vulns-chat-with-code/) does not seem to be the case. 

### Why did you only test OpenAI's ChatGPT plugins? Why not other platforms? 
Our intention is to study the plugin ecosystem in LLM platforms in general and not to focus on a particular platform. We decided to investigate OpenAI's plugin ecosystem as a case study because it has the most mature plugin ecosystem. Other platforms, such as Google Bard, have [announced plans](https://techcrunch.com/2023/05/10/google-launches-a-smarter-bard/) to integrate a plugin ecosystem, but have not provided an implementation yet. 

### What kind of risks are users currently exposed to? 
We uncover plugins that concretely demonstrate the potential for the issues that we outline in our attack taxonomy to manifest in practice. This does not necessarily mean that the plugins are malicious. However, considering the potential for attacks, our findings demonstrate that users are exposed to a number of risks. For example, plugins could steal their credentials, steal their chat history, hijack their interaction with the LLM platform, or trick them by masquerading as other plugins. Again, we stress the emphasis on the word "could" rather than "are"; we did not assess whether any plugins are performing adversarial actions.

### What can users do in the meantime to protect themselves?
Plugins are still in their beta phase and need to be enabled in user settings before they can be used. Users also need to enable plugins for a chat session before using them. These two restrictions limit the proliferation of plugins and consequently the potential for harm to users. Ideally, users should refrain from using plugins until the platform matures. However, users who have enabled plugins should be careful during their interactions. For example, users should restrict their plugin use to well-known services and avoid sharing personal and sensitive information in any chat session where plugins are enabled. If the plugin's behavior seems suspicious, they should immediately stop using it and report it to OpenAI. 

### What can plugins do to provide users a safe experience?
Plugins could start by following the optional suggestions provided by OpenAI. For example, OpenAI suggests that plugins implement [API request rate limits](https://platform.openai.com/docs/plugins/production/rate-limits), build [confirmation flows](https://platform.openai.com/docs/plugins/introduction) for requests that might alter user data (e.g., through POST requests), [use OAuth](https://platform.openai.com/docs/plugins/review/plugin-store) if the plugin takes an action on user's behalf, [not use non-OpenAI generative image models](https://platform.openai.com/docs/plugins/review/plugin-store), and use an allow list that only [allows traffic from the IP address range specified by OpenAI](https://platform.openai.com/docs/plugins/production/faq).  

Plugins should also thoroughly test their plugins. With such testing, developers might uncover problems with the OpenAI plugin ecosystem. Such problems can then be brought to OpenAI's attention so that they can be fixed. 

### Did you disclose your findings to OpenAI?
We disclosed the plugins named in our manuscript, which demonstrate the potential to pose a risk, to both OpenAI and their developers. OpenAI responded that they appreciate our effort in keeping the platform secure but have determined that the issues do not pose a security risk to the platform. However, we clarified to them that our assessment of these issues is that they pose a risk to users, plugins, and the LLM platform and should be seriously considered by OpenAI. 

Upon disclosing to plugin authors, we learned that in at least one case the plugin developer also disclosed the situation to OpenAI because OpenAI (not them) were in the position to fix the issue, but OpenAI did not.

For issues related to the core LLM, e.g., hallucination, ignoring instructions, OpenAI suggested that we report them to a [different forum](https://openai.com/form/model-behavior-feedback) so that their researchers can address them, which we also did.

### What are the ethical implications of your research?
In evaluating the ethics and morality of this research, we drew from both consequentialist and deontological traditions. From our analysis, we determined that the benefits of conducting our research, including developing our analysis framework, analyzing the potential for attacks within the OpenAI's ChatGPT ecosystem, and (eventually) sharing our results provided significant benefits to society and to users. Contributing to this decision was the fact that LLM-based systems are evolving at an incredibly rapid rate and researchers are continuing to discover vulnerabilities (which means that, if defensive directions are not developed, adversaries could also discover vulnerabilities).   

Further, we determined that it was important to give OpenAI advance notice about our findings and, hence, we disclosed this to OpenAI before disclosing these results publicly. While we did not mount any attacks ourselves, we did evaluate the potential for plugins to implement attacks. Hence, while one might argue that it is not necessary to disclose our findings to plugin manufacturers, we believe that they have a right to know about findings directly relevant to their products before the public, and hence we have informed plugin authors about our results and findings with respect to their plugins. We provide more details of our ethical analysis in Appendix B in the paper. 


         

## Research Team 
[Umar Iqbal](https://umariqbal.com) (Washington University in St. Louis)  
[Tadayoshi Kohno](https://homes.cs.washington.edu/~yoshi/) (University of Washington)  
[Franziska Roesner](https://www.franziroesner.com/) (University of Washington)   

## Funding 
This work was supported in part by the National Science Foundation under grant number CNS-2127309 (Computing Research Association for the CIFellows 2021 Project) and by the Tech Policy Lab at the University of Washington.




## Citation
```
@inproceedings{Iqbal24OpenAIPluginAnalysisAIES,
  title     = {LLM Platform Security: Applying a Systematic Evaluation Framework to OpenAI's ChatGPT Plugins},
  author    = {Umar Iqbal and Tadayoshi Kohno and Franziska Roesner},
  booktitle = {Proceedings of the 2024 AAAI/ACM Conference on AI, Ethics, and Society (AIES)},
  year      = {2024}
}
```
