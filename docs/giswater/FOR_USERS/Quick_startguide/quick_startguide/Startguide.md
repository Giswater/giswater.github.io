<script>
    var style = document.createElement('style');
    style.innerHTML = `
        .wy-nav-content {
            width: 100% !important;
            max-width: 100% !important;
            margin: 0 auto !important;
        }
    `;
    document.head.appendChild(style);
</script>

# Steps to create your first project

## Creating Schema and project using Giswater plugin on Qgis:

Hereafter you can find how to create an easy fast-start, considering you have all the programs, and an **adequate DB connection** (all required extensions for the plugin to work were added on the particular DB):

!!! note
       NOTICE: In order to make your work easy, we recommend having installed the example project.
        By having it you can check any moment what you want in order to solve some doubts you may have

**1. Create your DB project schema [Create DB project schema] by choosing your [LANG] and [EPSG]:**
Select empty project (without sample data or inp files)

!!! tip
       TIP: You need a PostgreSQL server with superadmin role to start working with giswater.

**2. Create your QGIS project file [Create QGIS project file] choosing the role_type**

!!! note
        NOTE 1: Be careful with your password!
        NOTE 2: As a starter role_type (basic) is easier to manage, since there are fewer functions and layers to control. Moreover, there are other roles, which enable more layer views, as well as access to more features of Giswater tools.

![Description of the image](assets\figure1_roles_projects.png)

## The following steps must be accomplished when starting an empty project:

!!! note
    Catalogs Layers ---> Mapzones Layers ---> Network Layers (this procedure will automatically fill 
    Hydraulics  EPA Layers) ---> Catalogs, Flwreg & Hydrology EPA Layers --->  Export2EPA ---> Check your
    simulation results

This order is exactly the same of the Project's Table of Content (ToC) in QGIS canvas, as you can see on the image below:

![Description of the image](assets\figure2_TOCGIWATER.png)

**3. Customize your own cat_feature elements, INSERTING or UPDATING or DELETING rows on *cat_feature table*: (*)**
Current elements are created by default upon the chosen [LANG], but all of them have the column *active* in false.
In order to activate them and start working with your project, you can INSERT new ones or UPDATE existing ones.
In case of UPDATE, you need to activate the feature (active=true) and you may modify *id*, *shortcut_key*, *child_layer* and *descript*.
If you will not use some features you can *UPDATE cat_feature SET active = false WHERE notUsedFeatures*!!!

!!! tip
        cat_feature table is the most important giswater project table, reuse existing ones by changing  `id`, 
        `shortcut_key`, `child_layer` could be your best approach in this start-from-scratch.
        if you modify child_layer column, the view related to that cat_feature is automaticaly renamed. 

        WARNING: On id column special characters are not allowed.

**4. Create your own material catalogs: (*)**

There are many material catalogs, but in this easy-to-start way you only need:  
Populate [Node material catalog] *cat_mat_node* table at least with one value filling mandatory columns from *id* to *descript*.    
Populate [Arc material catalog] *cat_mat_arc* table at least with one value filling mandatory columns from *id* to *descript*.

**5. Create your own feature catalogs: (*)**

There are many catalogs, but in this easy-to-start way you only need to:    
Populate [Node catalog], *cat_node* table with at least one value,  
- filling mandatory columns from *id* to *text* on ws projects  
- filling mandatory column *id* on ud projects  
Populate [Arc catalog], *cat_arc* table with at least one value,    
- filling mandatory columns from *id* to *text* on ws projects  
- filling mandatory columns *id*, *shape* and *geom1* on ud projects   

!!! tip
        TIP: On `ws projects`, `matcat_id` and feature catalog (`arctype_id`, `nodetype_id`) are mandatory.  
        On `ud projects`, `matcat_id` and feature catalog (`arc_type`, `node_type`) are not mandatory. In this  
        case we recommend to set this values directy on element (columns are ready to receive this info as well).  

**6. Start with mapzones [INVENTORY][Map zones] group: (*)**

Use [START EDITION] button from QGIS toolbar In this start form scratch, you can work only with the exploitation layer filling *expl_id*, *name*, *macroexpl_id* & *active*.    
Rest of mapzones (*municipality*, *sector*, *dma*, *presszone*(ws) or *dqa*(ws) may be created later.   
Use [CLOSE EDITION] to save changes.

!!! tip
    TIP: active field is used everywhere in Giswater. You always need to activate it in order to 
    work with elements located in a mapzone.

**7. Insert your first node:**

Click on **[ADD POINT BUTTON]** of giswater plugin and select one value defined on step-3.  
Start typing on *Nodecat_id* field and the values created on the catalog (step-5) will appear. **[ACCEPT]**

!!! note
    NOTE: If you do not see the node on canvas:
      Check your filters [SELECTOR BUTTON] of giswater plugin according with the selected state and exploitation.  
      Check `v_edit_node` qgis layer simbology and scale visibility depending value. 
 
**8. Insert your second node:**

Repeat step-7.

**9. Insert your first arc:**

Click on **[ADD LINE BUTTON]** of giswater plugin and select one value defined on step-3.   
Be careful with topological rules. Arc start & end vertex must be snapped to a node, but it can't be the same one.  
Start typing on *Arccat_id* fields and the values created on the catalog (step-5) will appear. **[ACCEPT]**

!!! note
     NOTE: If you do not see the arc on canvas:  
       Check your filters [SELECTOR BUTTON] of giswater plugin according with the selected state and exploitation.  
       Check v_edit_arc qgis layer simbology and scale visibility depending value. 
 
**10. Insert your second arc:**

In this case, if there is no end-node to snap, you can continue as shown:   
Click on **[CONFIG BUTTON]** of giswater plugin:    
on [tab Basic] look for *Automatic node insert as arc endpoint* and check it, in order to enable this option.   
on [tab Feature cat] look for Node Catalog, select one from combo and check it, in order to select it as default.   
Repeat step-9, now without end-node snnaped.   

!!! note
     NOTE: If things went well, you will see on canvas a new pipe and new node. 
 
(*) See project example for details !!!

Further complementary information can be found in the manual Sections: [2.5 Creation of the schema](../../Users_manual/2-Necessary_software/2.Necessary_software.md) & [6. How to digitalize the network](../../Users_manual/6-Digitalization/Digitalize_network.md) 

