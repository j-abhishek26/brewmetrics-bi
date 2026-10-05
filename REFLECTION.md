\# Reflection: AI-Assisted, Version-Controlled BI Engineering



Developing the BrewMetrics BI solution using Power BI Projects (.pbip) and 

GitHub Copilot fundamentally shifted my approach from traditional report 

building to modern software engineering practices.



GitHub Copilot proved highly effective for generating baseline DAX syntax, 

boilerplate aggregation patterns, and standard measure templates. It saved 

significant time during the initial drafting of each measure. However, it 

consistently struggled with tabular model filter context and Star Schema 

nuances. For instance, Copilot repeatedly suggested filtering fact tables 

directly rather than dimension tables and failed to account for row context 

removal in RANKX calculations. Across all four measures, I had to manually 

correct filter context issues, replace arithmetic division with DIVIDE for 

error safety, and restructure time intelligence functions to reference the 

proper Date dimension. Human understanding of DAX evaluation context remains 

essential for production-ready measures.



Adopting a strict version-controlled workflow transformed the development 

lifecycle. Traditional single-file .pbix development makes iterations opaque 

and rollbacks painful. With .pbip and TMDL, every relationship change, 

measure addition, and visual update was modular, auditable, and traceable 

through Git commits. This disciplined approach ensures enterprise data models 

remain robust, maintainable, and fully collaborative across teams.

