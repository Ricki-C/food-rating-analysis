<p>
Contributor: Ricki Chen
</p>

<h1>Introduction</h1>
<p>
  When users browse recipes online, ratings often serve as a quick summary of how successful a recipe is in practice. A high rating suggests that a recipe is not only tasty, but also feasible and satisfying for people who actually cooked it. This raises an important question: what aspects of a recipe tend to lead to higher user ratings?
</p>

<p>
 Two characteristics may play a key role. The first is recipe complexity, such as how long a recipe takes to prepare. Recipes that require too much time or effort may discourage users, while overly simple recipes may fail to meet expectations. The second is nutritional content, including calories, fat, sugar, and sodium, which can shape users’ perceptions of health and overall quality.
</p>

<p>
 Rather than treating these factors separately, this project examines how they work together to influence user ratings. This dataset contains recipes and ratings from <a href = "https://www.food.com/">Food.com</a>. It was originally scraped and used by the authors of this <a href = "https://cseweb.ucsd.edu/~jmcauley/pdfs/emnlp19c.pdf">recommender systems paper</a>. I explore <strong>how the complexity of recipes and their nutritional characteristics influence user ratings</strong>.
</p>

<h1>Data</h1>
<p>
  The dataset is sourced from Food.com and was originally scraped and released by the authors of a recommender systems study.
</p>

<h2>Recipes</h2>
<p>The raw dataset has 83,782 rows and 12 columns.</p>

<table>
  <thead>
    <tr>
      <th>Column</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>name</code></td><td>Recipe name</td></tr>
    <tr><td><code>id</code></td><td>Recipe ID</td></tr>
    <tr><td><code>minutes</code></td><td>Minutes to prepare recipe</td></tr>
    <tr><td><code>contributor_id</code></td><td>User ID who submitted this recipe</td></tr>
    <tr><td><code>submitted</code></td><td>Date recipe was submitted</td></tr>
    <tr><td><code>tags</code></td><td>Food.com tags for recipe</td></tr>
    <tr><td><code>nutrition</code></td><td>Nutrition info: [calories (kcal), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]. PDV = “percent daily value”.</td></tr>
    <tr><td><code>n_steps</code></td><td>Number of steps in recipe</td></tr>
    <tr><td><code>steps</code></td><td>Text for recipe steps, in order</td></tr>
    <tr><td><code>description</code></td><td>User-provided description</td></tr>
  </tbody>
</table>


<h2>Ratings</h2>
<p>The raw dataset has 731927 rows, 5 columns</p>
<table>
 <thead>
  <tr>
   <th>Column</th>
   <th>Description</th>
  </tr>
 </thead>

 <tbody>
   <tr><td><code>user_id</code></td><td>User ID</td></tr>
   <tr><td><code>recipe_id</code></td><td>Recipe ID</td></tr>
   <tr><td><code>date</code></td><td>Date of interaction</td></tr>
   <tr><td><code>rating</code></td><td>Rating given</td></tr>
   <tr><td><code>review</code></td><td>Review text</td></tr>
 </tbody>
</table>

<p>
Given the datasets, I am investigating <strong>how the complexity of recipes and their nutritional characteristics influence user ratings</strong>. To quantify recipe complexity, we use preparation time (<code>minutes</code>) and number of steps (<code>n_steps</code>) as proxies for the effort required to prepare a recipe. To facilitate the analysis of nutritional characteristics, we separated the values in the <code>nutrition</code> column into their corresponding numeric components, including calories and several nutrients measured as percentage daily value (PDV), such as total fat, sugar, sodium, protein, saturated fat, and carbohydrates. These nutritional variables are treated as quantitative descriptors. To evaluate the users' satisfaction with recipes, I use <code>average rating</code> for each unique recipe. By examining the relationships among these variables, we aim to better understand how effort-related and nutritional factors relate to user preferences on online recipe platforms, which could help contributors on Food.com improve their recipes to meet the public’s needs.
</p>


<h1>Data Cleaning and Exploratory Data Analysis</h1>

<p>To improve the efficiency and clarity of the analysis, I performed the following data cleaning steps.</p>

<!-- I just want to try to use a comment. Igmore it lol -->
<ol>

   <li>Inner merge the recipes and interactions datasets on <code>id</code> and <code>recipe_id</code>.
    <ul>
      <li>
        This step matches the unique recipes with their rating and review. 
      </li>
    </ul>
   </li>

  <li>Check the data types of all columns
    <ul>
      <li>
        This step helps me to conduct appropriate analysis.
      </li>
    </ul>
  </li>

  <li>Drop <code>id</code> column
      <ul>
        <li>
          This step drop the redundant column, creating a cleaner dataframe.
        </li>
      </ul>
  </li>

  <li>Check the missingness and impute appropriate elements
    <ul>
      <li>
        Missing values were observed in a small number of text-based columns, including <code>review</code>, <code>name</code>, and <code>description</code>. No imputation was performed, as missing values in text-based columns do not have meaningful substitutes.
      </li>
    </ul>
  </li>

  <li>Split the nutrition column into senven separate columns, each representing a different nutritional attribute,  including calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates.
    <ul>
      <li>
        This transformation allows each nutritional attribute to be analyzed individually and used as a numerical feature in subsequent analysis and modeling.
      </li>
    </ul>
  </li>

  <li>Add <code>avg_rating</code> column, which respresents the average rating for each unique recipe.
    <ul>
      <li>
        The average_rating variable represents the mean rating received by each recipe across all user interactions, providing a recipe-level measure of overall user evaluation.
      </li>
    </ul>
  </li>

  <li>Convert submitted and date to datetime
    <ul>
      <li>
        I convert those two columns into datatime, so I can use them to analysis the trends.
      </li>
    </ul>
  </li>

</ol>

<h2>Data Cleaning Result Dataframe</h2>
<iframe
  src="data_and_analysis\assets\cleaned_df_show.html"
  width="800"
  height="600"
  frameborder="0">
</iframe>



