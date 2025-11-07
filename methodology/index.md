---
layout: page
background_image: "/assets/images/headers/childsboyasagreement.webp"
imgaria: "Rurality agreement map across 8 of the most cited definitions"
title:  "Methodology"
byline: "This research employs a sequential quantitative, descriptive, and correlational design. Quantitative research is a paradigm that tests objective theories by examining the relationship among variables or groups. Descriptive research explores the aspects of a specific variable without proposing relationships between variables, correlation, or cause and effect -- it focuses on describing or measuring a  specific phenomenon or group."
seo_keywords: "methodology, sequantial, quantitative, quant"
seo_description: ""
---

<section class="grid split">
  <div>
    <figure>
      <img src="/assets/images/method/seq_quant.webp" width="90%" />
      <figcaption>Sequential Quantitative Process: recreate conditions of a previous study or technical description, statistically evaluate and confirm the results, expand, enhance, or experiment with the initial study being the foundation, evaluate the results.</figcaption>
    </figure>
  </div>
  <div class="text-container">
    <header class="centered">
      <h3>A Sequential Quantitative Geospatial Analysis</h3>
    </header>
    <div>
      <p>
        The geographical extent of this phase includes the Continental 48 United States and their entire population. This research does not conduct any sampling.  The locale definitions of the National Center for Education Statistics (NCES) serve as the classification system for census blocks. As of 2019 the NCES locales categorize U.S. territory into four types of areas: City, Suburban, Town, and Rural. Each type of area contains three subtypes that can be fully collapsed into a fundamental urban-rural dichotomy or expanded into a more detailed collection of 12 distinct categories. Size differentiates a subtype in the case of city and suburban assignments, and proximity differentiates in the case of town and rural assignments.
      </p>
      <p>
      The United States Census Bureau partitions statistical areas into census blocks bounded by visible features such as roads, streams, and railroad tracks and by nonvisible boundaries such as selected property lines and city, township, school district, and county limits and short line-of-sight extensions of streets and roads. The National Center for Education Statistics divides areas based on population size or proximity to populated areas.
      </p>
    </div>
  </div>
</section>

<section class="grid split">
  <div>
    <section class="stripe centered">
      <h3>Phase 1: Geospatial Processing</h3>
    </section>
    <p>
      The rural and urban structures of the National Center for Education Statistics and the United States Census Bureau differ. For each State's 118th Congressional District administrative divisions, all legal boundaries and names are current as of January 1, 2020, except for the 118th Congressional Districts and State Legislative Districts, which are current as of January 1, 2023. The data for the administrative divisions was obtained through the USCB Census Mapping Files file transfer protocol archive on the bureau’s website in a Topologically Integrated Geographic Encoding and Referencing (TIGER) and TIGER/Line in shapefile format. The spatial analysis classifies a given census block according to the NCES codes using the desktop version of QGIS, version 3.3.0 “Hertogenbosch”.
    </p>
  </div>
  <div>
    <figure>
      <img src="/assets/images/method/block_partition.webp" width="90%" />
      <figcaption>Detecting geometry intersections and computing the percent area where the polygons intersect and creates a
separate vector layer containing each intersection area's GEOID and LOCALE attributes.</figcaption>
    </figure>
  </div>
</section>

<section>
  <p>
    Using the Python programming language, QGIS’ API, and QGIS’ Software Development Kit (SDK), a script loads the NCES and USCB shapefiles as Vector Layers containing the census block and NCES features (polygons). The script then stacks the layers into
a Map Layer, with the NCES layer being the first layer and the USCB layer being the second layer – allowing spatial boundary intersection calculations. For each polygon in the USCB shapefile, the script loads each polygon into a thread-safe queue. Thread-safe queues enable multiple instances of the script to read data from it, allowing the geospatial analysis to execute more efficiently and retry a task should one fail. Multiple instances of the script, “threads,” then pull the USCB polygons from a queue. Each thread computes the centroid of the polygons by partitioning them into triangles. The weighted sum of each triangle's x and y coordinates determines the centroid of the entire
polygon. The script checks if the geometry of the centroid of each USCB polygon area is within any of the NCES polygon areas. A second script detects if the geometry of the USCB polygon crosses multiple NCES polygons. Lastly, a third script computes the percent area where the polygons intersect and creates a separate vector layer containing each intersection area's GEOID and LOCALE attributes. Three new attributes are added and set for each USCB feature. The “LOCALE” attribute from the NCES polygon in which the centroid of the USCB polygon lies “centroid_nces_code.” For each NCES polygon the USCB polygon crosses, a comma-delimited list of each NCES “LOCALE” attribute “nces_cross.” Lastly, the area percent for each polygon crosses “nces_cross_pct.” 
  </p>
</section>

<section class="stripe centered">
  <h3>Data Evaluation</h3>
</section>

<section class="text-container grid three-columns">
  <div>
    <h3 class="centered">Pearson's Test</h3>
    <p>
    A Person’s test for kurtosis describes a distribution's characteristics. Kurtosis measures whether data is heavy-tailed or light-tailed relative to a normal distribution. A distribution with over-dispersed data relative to a normal distribution will have high kurtosis and tend to have heavy tails or outliers – a leptokurtic distribution. Under-dispersed data will have low kurtosis and tend to have a light tail or lack of outliers – a platykurtic distribution.
    </p>
  </div>
  <div>
    <h3 class="centered">Hartigan Dip Test of Unimodality</h3>
    <p>
      A Hartigan Dip Test of Unimodality to determines if multimodality is present in the distribution. The dip test measures multimodality in a sample by the maximum difference, over all sample points, between the empirical distribution function and the unimodal distribution function that minimizes that maximum difference. The uniform distribution is the asymptotically least favorable unimodal distribution, and the distribution of the test statistic is determined asymptotically and empirically  when sampling from the uniform.
    </p>
  </div>
  <div>
    <h3 class="centered">Mann-Whitney U test</h3>
    <p>
      A Mann-Whitney U test identifies whether the census blocks and responses from the NCES originate from the same population. The Mann-Whitney U is also applied to the US Census Bureau classification of census blocks and the NCES classification to identify geospatial alignment. The Mann-Whitney U test has no dependence on normality and its ability to test ordinal data.
    </p>
  </div>
</section>

<section class="stripe">
  <h3>Phase 2: Aligning Education Institutions and Modeling</h3>
</section>

<section class="grid split">
  <div>
    <figure>
      <img src="/assets/images/method/phase1_artifact.webp" width="80%" />
      <figcaption>Phase 1 Artifact: census blocks falling into locales being broken into smaller blocks to fit within each locale and
merged into the blocks list.</figcaption>
    </figure>
  </div>
  <div>
    <p>
       Phase 2 applies a correlational quantitative design, seeking to identify the relationship between the variables and the NCES locale code for a given area and model the population using the information collected from the observed population. The geographical extent for phase 2 maintains the same scope as phase 1.
    </p>
    <p>
      School demographic data originates from the American Community Survey Education
      Tabulation (ACS-ED). The ACS-ED is a custom tabulation of the ACS produced for the
      National Center of Education Statistics (NCES) by the U.S. Census Bureau. The surveys provide a collection of social, economic, demographic,
      and housing characteristics for school systems, school-age children, and the parents of schoolage children. In addition to focusing on school-age children, the ACS-ED provides enrollment iterations for children enrolled in public schools. The data profiles include percentages (along 
      with associated margins of error) that allow for comparison of school district-level conditions
      across the U.S. All information the data profiles contain is in the public domain. 
    </p>
    <p>
      For feature selection in the classification model, classification and regression tree
      (CART) models effectively explain any variance in a response variable. CART models are non-parametric and output a decision tree for classification or regression. A CART algorithm selects the optimal decision threshold for a variable based on recursive partitioning, testing the potential value of different thresholds for each predictor, and implementing the most
      valuable until further splitting no longer improves discrimination. Combined with
      ensemble techniques, creating multiple models and combining them to improve accuracy, CART
      models discover meaningful interactions and non-linear effects of the predictors.
    </p>
  </div>
</section>