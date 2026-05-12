    # read in the data 
    spotify <- read_csv("https://raw.githubusercontent.com/Demibolt007/Spotify-Streaming-Insights-2010-2019/main/Spotify%20Dataset.csv")

    # take a look at the data set
    glimpse(spotify)

    ## Rows: 599
    ## Columns: 25
    ## $ Song                   <chr> "3", "43776", "#Beautiful", "#SELFIE", "#thatPO…
    ## $ Artist                 <chr> "Britney Spears", "Beyoncé", "Mariah Carey", "T…
    ## $ Genre                  <chr> "Dance Pop", "Dance Pop", "Dance Pop", "Electro…
    ## $ Year                   <dbl> 2010, 2015, 2013, 2014, 2013, 2018, 2011, 2017,…
    ## $ Streams                <dbl> 339473453, 665765558, 245400167, 382199619, 473…
    ## $ `In Spotify Playlists` <dbl> 2612, 5415, 1796, 2988, 3741, 1800, 2442, 3983,…
    ## $ `On Spotify Charts`    <dbl> 258, 396, 317, 331, 444, 274, 326, 421, 197, 27…
    ## $ `Billboard Rankings`   <dbl> 192, 31, 12, 109, 101, 6, 283, 12, 19, 38, 15, …
    ## $ `In Apple Playlists`   <dbl> 32497, 29766, 37077, 3762, 38461, 5969, 2868, 3…
    ## $ `On Apple Charts`      <dbl> 69, 31, 12, 109, 101, 6, 55, 12, 19, 89, 15, 18…
    ## $ `In Deezer Playlists`  <dbl> 7444, 1, 10, 305, 1397, 19, 5758, 51, 318, 2094…
    ## $ `In Deezer Charts`     <dbl> 164, 34, 33, 3, 4, 46, 191, 1, 29, 13, 24, 28, …
    ## $ `In YouTube Playlists` <dbl> 5718, 17576, 15160, 38113, 23843, 28523, 11754,…
    ## $ `On Shazam Charts`     <dbl> 127, 168, 319, 149, 320, 292, 339, 58, 200, 245…
    ## $ Bpm                    <dbl> 135, 136, 107, 128, 128, 160, 63, 107, 145, 120…
    ## $ Decibel                <dbl> -2, -5, -5, -3, -6, -5, -7, -4, -7, -6, -5, -6,…
    ## $ Mode                   <chr> "Major", "Major", "Major", "Major", "Minor", "M…
    ## $ Energy                 <dbl> 71, 71, 76, 92, 61, 84, 38, 80, 61, 47, 88, 62,…
    ## $ Danceability           <dbl> 70, 75, 68, 79, 80, 58, 30, 82, 53, 77, 43, 76,…
    ## $ Liveness               <dbl> 14, 13, 31, 8, 7, 10, 7, 15, 23, 39, 21, 9, 21,…
    ## $ Valence                <dbl> 79, 56, 45, 66, 40, 50, 26, 63, 53, 34, 25, 52,…
    ## $ Duration               <dbl> 213, 214, 200, 184, 280, 190, 274, 226, 195, 23…
    ## $ Acousticness           <dbl> 5, 1, 29, 1, 0, 13, 38, 3, 23, 29, 0, 1, 1, 31,…
    ## $ Speechiness            <dbl> 5, 13, 4, 25, 6, 22, 3, 8, 6, 5, 4, 18, 3, 3, 3…
    ## $ Popularity             <dbl> 62, 72, 51, 65, 68, 85, 60, 85, 65, 80, 41, 65,…

    # the chosen 5 predictors will be
    # danceability, energy, valnece, loudness, and mode. With mode beeing the categorical variable 

    spotify <- spotify %>%
      mutate(
        mode_yn = if_else(Mode == "Major", "Yes", "No")  # Yes = major, No = minor
      )
    glimpse(spotify)

    ## Rows: 599
    ## Columns: 26
    ## $ Song                   <chr> "3", "43776", "#Beautiful", "#SELFIE", "#thatPO…
    ## $ Artist                 <chr> "Britney Spears", "Beyoncé", "Mariah Carey", "T…
    ## $ Genre                  <chr> "Dance Pop", "Dance Pop", "Dance Pop", "Electro…
    ## $ Year                   <dbl> 2010, 2015, 2013, 2014, 2013, 2018, 2011, 2017,…
    ## $ Streams                <dbl> 339473453, 665765558, 245400167, 382199619, 473…
    ## $ `In Spotify Playlists` <dbl> 2612, 5415, 1796, 2988, 3741, 1800, 2442, 3983,…
    ## $ `On Spotify Charts`    <dbl> 258, 396, 317, 331, 444, 274, 326, 421, 197, 27…
    ## $ `Billboard Rankings`   <dbl> 192, 31, 12, 109, 101, 6, 283, 12, 19, 38, 15, …
    ## $ `In Apple Playlists`   <dbl> 32497, 29766, 37077, 3762, 38461, 5969, 2868, 3…
    ## $ `On Apple Charts`      <dbl> 69, 31, 12, 109, 101, 6, 55, 12, 19, 89, 15, 18…
    ## $ `In Deezer Playlists`  <dbl> 7444, 1, 10, 305, 1397, 19, 5758, 51, 318, 2094…
    ## $ `In Deezer Charts`     <dbl> 164, 34, 33, 3, 4, 46, 191, 1, 29, 13, 24, 28, …
    ## $ `In YouTube Playlists` <dbl> 5718, 17576, 15160, 38113, 23843, 28523, 11754,…
    ## $ `On Shazam Charts`     <dbl> 127, 168, 319, 149, 320, 292, 339, 58, 200, 245…
    ## $ Bpm                    <dbl> 135, 136, 107, 128, 128, 160, 63, 107, 145, 120…
    ## $ Decibel                <dbl> -2, -5, -5, -3, -6, -5, -7, -4, -7, -6, -5, -6,…
    ## $ Mode                   <chr> "Major", "Major", "Major", "Major", "Minor", "M…
    ## $ Energy                 <dbl> 71, 71, 76, 92, 61, 84, 38, 80, 61, 47, 88, 62,…
    ## $ Danceability           <dbl> 70, 75, 68, 79, 80, 58, 30, 82, 53, 77, 43, 76,…
    ## $ Liveness               <dbl> 14, 13, 31, 8, 7, 10, 7, 15, 23, 39, 21, 9, 21,…
    ## $ Valence                <dbl> 79, 56, 45, 66, 40, 50, 26, 63, 53, 34, 25, 52,…
    ## $ Duration               <dbl> 213, 214, 200, 184, 280, 190, 274, 226, 195, 23…
    ## $ Acousticness           <dbl> 5, 1, 29, 1, 0, 13, 38, 3, 23, 29, 0, 1, 1, 31,…
    ## $ Speechiness            <dbl> 5, 13, 4, 25, 6, 22, 3, 8, 6, 5, 4, 18, 3, 3, 3…
    ## $ Popularity             <dbl> 62, 72, 51, 65, 68, 85, 60, 85, 65, 80, 41, 65,…
    ## $ mode_yn                <chr> "Yes", "Yes", "Yes", "Yes", "No", "Yes", "No", …

    spotify <- spotify %>% 
      mutate(
        Mode = as.factor(mode_yn)
      )
    glimpse(spotify)

    ## Rows: 599
    ## Columns: 26
    ## $ Song                   <chr> "3", "43776", "#Beautiful", "#SELFIE", "#thatPO…
    ## $ Artist                 <chr> "Britney Spears", "Beyoncé", "Mariah Carey", "T…
    ## $ Genre                  <chr> "Dance Pop", "Dance Pop", "Dance Pop", "Electro…
    ## $ Year                   <dbl> 2010, 2015, 2013, 2014, 2013, 2018, 2011, 2017,…
    ## $ Streams                <dbl> 339473453, 665765558, 245400167, 382199619, 473…
    ## $ `In Spotify Playlists` <dbl> 2612, 5415, 1796, 2988, 3741, 1800, 2442, 3983,…
    ## $ `On Spotify Charts`    <dbl> 258, 396, 317, 331, 444, 274, 326, 421, 197, 27…
    ## $ `Billboard Rankings`   <dbl> 192, 31, 12, 109, 101, 6, 283, 12, 19, 38, 15, …
    ## $ `In Apple Playlists`   <dbl> 32497, 29766, 37077, 3762, 38461, 5969, 2868, 3…
    ## $ `On Apple Charts`      <dbl> 69, 31, 12, 109, 101, 6, 55, 12, 19, 89, 15, 18…
    ## $ `In Deezer Playlists`  <dbl> 7444, 1, 10, 305, 1397, 19, 5758, 51, 318, 2094…
    ## $ `In Deezer Charts`     <dbl> 164, 34, 33, 3, 4, 46, 191, 1, 29, 13, 24, 28, …
    ## $ `In YouTube Playlists` <dbl> 5718, 17576, 15160, 38113, 23843, 28523, 11754,…
    ## $ `On Shazam Charts`     <dbl> 127, 168, 319, 149, 320, 292, 339, 58, 200, 245…
    ## $ Bpm                    <dbl> 135, 136, 107, 128, 128, 160, 63, 107, 145, 120…
    ## $ Decibel                <dbl> -2, -5, -5, -3, -6, -5, -7, -4, -7, -6, -5, -6,…
    ## $ Mode                   <fct> Yes, Yes, Yes, Yes, No, Yes, No, Yes, No, No, N…
    ## $ Energy                 <dbl> 71, 71, 76, 92, 61, 84, 38, 80, 61, 47, 88, 62,…
    ## $ Danceability           <dbl> 70, 75, 68, 79, 80, 58, 30, 82, 53, 77, 43, 76,…
    ## $ Liveness               <dbl> 14, 13, 31, 8, 7, 10, 7, 15, 23, 39, 21, 9, 21,…
    ## $ Valence                <dbl> 79, 56, 45, 66, 40, 50, 26, 63, 53, 34, 25, 52,…
    ## $ Duration               <dbl> 213, 214, 200, 184, 280, 190, 274, 226, 195, 23…
    ## $ Acousticness           <dbl> 5, 1, 29, 1, 0, 13, 38, 3, 23, 29, 0, 1, 1, 31,…
    ## $ Speechiness            <dbl> 5, 13, 4, 25, 6, 22, 3, 8, 6, 5, 4, 18, 3, 3, 3…
    ## $ Popularity             <dbl> 62, 72, 51, 65, 68, 85, 60, 85, 65, 80, 41, 65,…
    ## $ mode_yn                <chr> "Yes", "Yes", "Yes", "Yes", "No", "Yes", "No", …

    # model for data
    spotify_model <- spotify %>%
      select(
        Popularity, # predictor variable, we are testing for popularity
        Danceability,
        Energy,
        Valence,
        Decibel,
        Mode # categorical predictor, 'Yes' = Major, 'No' = Minor
      )

    glimpse(spotify_model)

    ## Rows: 599
    ## Columns: 6
    ## $ Popularity   <dbl> 62, 72, 51, 65, 68, 85, 60, 85, 65, 80, 41, 65, 60, 81, 7…
    ## $ Danceability <dbl> 70, 75, 68, 79, 80, 58, 30, 82, 53, 77, 43, 76, 55, 42, 5…
    ## $ Energy       <dbl> 71, 71, 76, 92, 61, 84, 38, 80, 61, 47, 88, 62, 68, 41, 6…
    ## $ Valence      <dbl> 79, 56, 45, 66, 40, 50, 26, 63, 53, 34, 25, 52, 16, 16, 2…
    ## $ Decibel      <dbl> -2, -5, -5, -3, -6, -5, -7, -4, -7, -6, -5, -6, -6, -7, -…
    ## $ Mode         <fct> Yes, Yes, Yes, Yes, No, Yes, No, Yes, No, No, No, Yes, No…

    # Energy plot
    ggplot(spotify_model, aes(Energy, Popularity)) + 
      geom_point(alpha = 0.5, color = "blue3") + 
      geom_smooth(method = 'lm', color = 'orange1') + 
      labs(
        title = "Popularity as Response to Energy",
        x = "Energy",
        y = "Popularity"
      )

![](figs/2.1-1.png)

    # Danceability plot
    ggplot(spotify_model, aes(Danceability, Popularity)) + 
      geom_point(alpha = 0.5, color = "blue3") + 
      geom_smooth(method = 'lm', color = 'orange1') + 
      labs(
        title = "Popularity as Response to Danceability",
        x = "Danceability",
        y = "Popularity"
      )

![](figs/2.2-1.png)

    # Valence plot
    ggplot(spotify_model, aes(Valence, Popularity)) + 
      geom_point(alpha = 0.5, color = "blue3") + 
      geom_smooth(method = 'lm', color = 'orange1') + 
      labs(
        title = "Popularity as Response to Valence",
        x = "Valence",
        y = "Popularity"
      )

![](figs/2.3-1.png)

    # Decibel plot
    ggplot(spotify_model, aes(Decibel, Popularity)) + 
      geom_point(alpha = 0.5, color = "blue3") + 
      geom_smooth(method = 'lm', color = 'orange1') + 
      labs(
        title = "Popularity as Response to Decibel",
        x = "Decibel",
        y = "Popularity"
      )

![](figs/2.4-1.png)

    # Mode plot
    ggplot(spotify_model, aes(Mode, Popularity, fill = Mode)) +
      geom_boxplot(alpha = 0.7) +
      labs(
        title = "Popularity as Response to Musical Mode",
        x = "Mode (Major / Minor)",
        y = "Popularity"
      ) +
      scale_fill_manual(values = c("Yes" = "skyblue", "No" = "pink"))

![](figs/2.5-1.png)

    # create the linear regression model for the data 
    pop_mod <- lm(
      Popularity ~ Energy + Danceability + Valence + Decibel + Mode,
      data = spotify_model
    )
    # take a look at the summary to be able to see the significance of each coefficient 
    summary(pop_mod)

    ## 
    ## Call:
    ## lm(formula = Popularity ~ Energy + Danceability + Valence + Decibel + 
    ##     Mode, data = spotify_model)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -68.612  -7.286   2.133   9.509  31.123 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  75.03882    6.31593  11.881   <2e-16 ***
    ## Energy       -0.11599    0.05104  -2.272   0.0234 *  
    ## Danceability  0.06368    0.05118   1.244   0.2139    
    ## Valence       0.01168    0.03328   0.351   0.7258    
    ## Decibel       0.60286    0.46382   1.300   0.1942    
    ## ModeYes      -0.45289    1.20948  -0.374   0.7082    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 14.59 on 593 degrees of freedom
    ## Multiple R-squared:  0.01263,    Adjusted R-squared:  0.004309 
    ## F-statistic: 1.518 on 5 and 593 DF,  p-value: 0.1823

    # 5 fold cross validation 
    set.seed(400)
    train_control <- trainControl(
      method = 'cv',
      number = 5 
    )
    # create the five different models
    # model 1, full model linear regression 
    full_spotify_lm <- train(
      Popularity ~ Energy + Danceability + Valence + Decibel + Mode, 
      data = spotify_model,
      method = 'lm',
      trControl = train_control
    )
    # view model 1 
    full_spotify_lm

    ## Linear Regression 
    ## 
    ## 599 samples
    ##   5 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (5 fold) 
    ## Summary of sample sizes: 480, 480, 478, 479, 479 
    ## Resampling results:
    ## 
    ##   RMSE      Rsquared    MAE     
    ##   14.69142  0.01292347  11.00862
    ## 
    ## Tuning parameter 'intercept' was held constant at a value of TRUE

    # model 2, reduced linear regression, using energy and danceability 
    subst_spotify_lm <- train(
      Popularity ~ Energy + Danceability,
      data = spotify_model,
      method = 'lm',
      trControl = train_control
    )
    #view model 2 
    subst_spotify_lm

    ## Linear Regression 
    ## 
    ## 599 samples
    ##   2 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (5 fold) 
    ## Summary of sample sizes: 479, 480, 478, 479, 480 
    ## Resampling results:
    ## 
    ##   RMSE      Rsquared    MAE     
    ##   14.58712  0.01419621  10.88228
    ## 
    ## Tuning parameter 'intercept' was held constant at a value of TRUE

    # model 3, random forest model
    spotify_rf <- train(
      Popularity ~.,
      data = spotify_model,
      method = 'rf',
      trControl = train_control,
      tuneLength = 5 
    )

    ## note: only 4 unique complexity parameters in default grid. Truncating the grid to 4 .

    # view model 3
    spotify_rf

    ## Random Forest 
    ## 
    ## 599 samples
    ##   5 predictor
    ## 
    ## No pre-processing
    ## Resampling: Cross-Validated (5 fold) 
    ## Summary of sample sizes: 480, 480, 478, 478, 480 
    ## Resampling results across tuning parameters:
    ## 
    ##   mtry  RMSE      Rsquared    MAE     
    ##   2     14.93217  0.01953001  11.25589
    ##   3     15.09819  0.01416068  11.45021
    ##   4     15.25434  0.01394883  11.57152
    ##   5     15.34531  0.01357961  11.67516
    ## 
    ## RMSE was used to select the optimal model using the smallest value.
    ## The final value used for the model was mtry = 2.

    # compare the 3 models 
    model_results <- resamples(list(
      FULL = full_spotify_lm,
      SUB = subst_spotify_lm,
      RF = spotify_rf
    ))
    # view the summary of the reuslt s
    summary(model_results)

    ## 
    ## Call:
    ## summary.resamples(object = model_results)
    ## 
    ## Models: FULL, SUB, RF 
    ## Number of resamples: 5 
    ## 
    ## MAE 
    ##          Min.  1st Qu.   Median     Mean  3rd Qu.     Max. NA's
    ## FULL 10.46340 10.51546 11.11676 11.00862 11.42481 11.52267    0
    ## SUB  10.44913 10.80964 10.83945 10.88228 10.92025 11.39295    0
    ## RF   10.22625 10.88926 11.04994 11.25589 11.56653 12.54747    0
    ## 
    ## RMSE 
    ##          Min.  1st Qu.   Median     Mean  3rd Qu.     Max. NA's
    ## FULL 13.06402 13.79991 14.94668 14.69142 15.64965 15.99682    0
    ## SUB  14.07383 14.22474 14.60068 14.58712 14.94779 15.08855    0
    ## RF   12.74217 13.44740 14.84457 14.93217 16.70537 16.92132    0
    ## 
    ## Rsquared 
    ##              Min.      1st Qu.     Median       Mean    3rd Qu.       Max. NA's
    ## FULL 0.0011247318 0.0024287740 0.01265655 0.01292347 0.01527083 0.03313647    0
    ## SUB  0.0026839821 0.0063160830 0.01000612 0.01419621 0.01295146 0.03902339    0
    ## RF   0.0001364608 0.0007814328 0.02887351 0.01953001 0.03000424 0.03785440    0

**Rationale for each model choice**

*For the first model, the Full Linear Regression Model, I chose this one
because it encompasses each of the variables in the model and allows us
to see how each of them effect the prediction probability for the
observed variable of population.*

*For the second model, the Subset Linear Regression Model, this model
takes a closer look at the two variables (Energy + Danceability) that
previously displayed the strongest influence on the observed variable.*

*For the third model, the Random Forest Model, this model looks at a
more tree-based, probability method. In other words, a more flexible,
non-linear approach to testing the data.*

    bwplot(model_results)

![](figs/4.2-1.png)

**Which Model Performs Best**

*Looking at the three different models, the RF (Random Forest) Model can
be seen with the lowest MAE, the lowest RMSE and the highest R^2 values.
secondly the FULL (Full Linear Regression) Model can be seen performing
moderately well across the same metrics, with a higher error value than
the RF Model, but still not bad. Lastly, the SUB (Subset Linear
Regression) Model can be seen performing the worst across all three
metrics. With this information we can conclude that the RF Model
performs the best as it consistently shows the lowest prediction error
and the highest explanation of influence across all three*

**Alternative Metrics**

*A different metric we may be able to use could be the adjusted R^2
value, this value can be preferred in some testing sets because it can
clear out some noise form the less influential predictors, bringing more
validity to the predictors with the most influence over the data*

**Implications of Predictions**

*Overall, when looking at our data we can see that song popularity can
be influenced by multiple interacting variables, with Energy and
Danceability consistently showing up as the strongest predictors. Some
of our models show that Popularity is not always a linear value, and
that the non linear predictors play a huge role in helping cancel out
some of the noise in the data set*
