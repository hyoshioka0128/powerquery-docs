--- 

title: Understanding the differences between standard and analytical dataflows 

description: Understanding the differences between standard and analytical dataflows 

author: radacad 

ms.service: powerquery 

ms.topic: conceptual 

ms.date: 05/11/2020 

ms.author: bensack 

 

--- 

 

# Understanding the differences between standard and analytical dataflows 

 

You can categorize dataflows in many ways. One of those ways is the difference between standard and analytical dataflows. Understanding this concept helps you create the dataflow for the right requirement. Dataflows create entities, and entities are of two types: standard and analytical. Based on the type of entity produced by the dataflow, we call the dataflow either a standard dataflow or an analytical dataflow. 

 

## Standard dataflow 

 

A dataflow by the standard definition is used to extract, transform, and load data to a destination. A standard dataflow’s destination must be the Common Data Service and the entities produces are database entities.  

 

Standard dataflows can be created through the Power Apps portal. 

 

![Creating a standard dataflow](media/analytical-standard-dataflows/create-standard-dataflow.png) 

 

One benefit of this type of dataflow is that any application that can connect to Common Data Service can work with the data, such as Power BI, Power Apps, Power Automate, Power Virtual Agent, Dynamics 365, and other applications. 

 

## Analytical dataflow 

 

An analytical dataflow stores its entities in storage optimized for analytics&mdash;Azure Data Lake Storage Gen2. Power Platform environments and Power BI workspaces provide customers with managed analytical storage location that's bundled with those product licenses. In addition, customers can link their organization’s Azure Data Lake storage Gen2 account as a destination for dataflows. 

 

Analytical dataflows are capable additional analytical features. For example, integration with Power BI’s AI features or use of computed entities which will be discussed later.  

 

You can create analytical dataflows in Power BI. By default, they'll load data to Power BI’s managed storage. But you can also configure Power Bi to store the data in the organization’s Azure Data Lake Storage Gen2. 

 

![Creating an analytical dataflow in Power BI](media/analytical-standard-dataflows/create-analytical-dataflow-powerbi.png) 

 

You can also create analytical dataflows in Power Apps and Dynamics 365 customer insights portals. When you're creating a dataflow in Power Apps portal, you can choose between Common Data Service manages analytical storage or in your organization’s Azure Data Lake storage Gen2 account. 

 

![Creating Analytical Dataflow in Power Platform](media/analytical-standard-dataflows/create-analytical-dataflow-power-platform.png) 

 

### AI Integration 

 

Sometimes, depending on the requirement, you might need to apply some AI and machine learning functions on the data through the dataflow. These functionalities are available in Power BI dataflows and require a Premium workspace. 

 

![AI insights in an analytical dataflow](media/analytical-standard-dataflows/dataflow-ai-functions.png) 

 

The following articles discuss how to use AI functions in a dataflow: 

 

- [Azure Machine Learning integration in Power BI](https://docs.microsoft.com/power-bi/service-machine-learning-integration) 

- [Cognitive Services in Power BI](https://docs.microsoft.com/power-bi/service-cognitive-services) 

- [Automated Machine Learning in Power BI](https://docs.microsoft.com/power-bi/service-machine-learning-automated) 

 

Note that the features listed above are Power BI specific and are not available when creating a dataflow in the Power Apps or Dynamics 365 customer insights portals.  

 

### Computed entities 

 

One of the reasons to use a computed entity is the ability to process large amounts of data. The computed entity helps in those scenarios. If you have an entity in a dataflow, and another entity in the same dataflow uses the first entity's output, this will create a computed entity. 

 

The computed entity helps with the performance of the data transformations. Instead of re-doing the transformations needed in the first entity multiple times, the transformation will be done only once in the computed entity. Then the result will be used multiple times in other entities. 

 

![Computed entity in an analytical dataflow](media/analytical-standard-dataflows/computed-entity-in-dataflow.png) 

 

To learn more about computed entities, see [Using computed entities on Power BI Premium](https://docs.microsoft.com/power-bi/service-dataflows-computed-entities-premium). 

 

Computed entities are available only in an analytical dataflow. 

 

## Standard vs. analytical dataflows 

 

The following table lists some differences between a standard entity and an analytical entity. 

 

| Operation               | Standard             | Analytical                    | 
| --------------------------------- | --- | ------------------------------------------------------------ | 
| How to create                     | Power Platform dataflows | Power BI dataflows<br />Power Platform dataflows by selecting the **Analytical Entity** checkbox when creating the dataflow | 
| Storage options                   | Common Data Service      | Azure Data Lake Storage Gen2 internal for the Power BI dataflows<br />Azure Data Lake Storage Gen2 external attached to the Power BI or Power Platform dataflows | 
| Power Query transformations       | Yes             |Yes                                                          | 
| AI functions                      | No              | Yes                                                          | 
| Computed entity                   | No              | Yes                                                          | 
| Can be used in other applications | Yes, through Common Data Service | Power BI dataflows: Only in Power BI<br />Power Platform dataflows or Power BI external dataflows: Yes, through Azure Data Lake Storage Gen2 | 
| Mapping to standard Entity        | Yes              | Yes                                                         | 
| Incremental load                  | Default incremental-load<br />Possible to change using the **Delete rows that no longer exist in the query output** checkbox at the load settings | Default full-load <br />Possible to set up incremental refresh by setting up the incremental refresh in the dataflow settings | 
| Scheduled Refresh                 | Yes              | Yes, the possibility of notifying the dataflow owners upon the failure | 
| | | |
 

## Scenarios to use each dataflow type 

 

Here are some sample scenarios and best practice recommendations for each type of dataflow. 

 

### Cross-platform usage&mdash;standard dataflow 

 

If your plan for building dataflows is to use stored data in multiple platforms (not only Power BI, but also other Power Platform services, Dynamics, and so on), a standard dataflow is a great choice. Standard dataflows store the data in Common Data Service, which you can access through many other platforms and services. 

 

### Heavy data transformations on large data tables&mdash;analytical dataflow 

 

Analytical dataflows are an excellent option for processing large amounts of data. Analytical dataflows are also enhancing the computing power behind the transformation. Having the data is stored in Azure Data Lake Storage Gen2 increases the writing speed to a destination. Compared to Common Data Service (which might have many rules to check at the time of data storage), Azure Data Lake Storage Gen2 is faster for read/write transactions on a large amount of data. 

 

### AI features&mdash;analytical dataflow 

 

If you're planning to use any AI functionalities through the data transformation stage, then an analytical dataflow is helpful because you can use all the supported AI features with this type of dataflow. 

 
