**Problem 1**

    #Read in the CSV files 
    renew_gen <- read_csv("https://ourworldindata.org/grapher/renewable-electricity-per-capita.csv")
    energy_use <- read_csv("https://ourworldindata.org/grapher/per-capita-energy-use.csv")
    renew_share <- read_csv("https://ourworldindata.org/grapher/share-electricity-renewables.csv")

    latest_year <- max(renew_gen$Year, na.rm = TRUE)
    latest_year_E <- max(energy_use$Year, na.rm = TRUE)

    renew_latest <- renew_gen %>%
      filter(Year == latest_year)

    energy_latest <- energy_use %>%
      filter(Year == latest_year_E)

    world_map <- map_data("world")

    renew_latest2 <- renew_latest %>%
      rename(country = Entity,
             renew_pc = `Renewable electricity per capita`)

    energy_latest2 <- energy_latest %>%
      rename(country = Entity,
             energy_pc = `Per capita energy consumption`)

    map_renew <- world_map %>%
      left_join(renew_latest2, by = c("region" = "country"))

    map_energy <- world_map %>%
      left_join(energy_latest2, by = c("region" = "country"))

    ggplot(map_renew, aes(x = long, y = lat, group = group, fill = renew_pc)) +
      geom_polygon(color = "black", size = 0.1) +
      scale_fill_gradient(low = "lightblue", high = "darkblue", na.value = "grey80") +
      labs(
        title = "Renewable Electricity Generation per Capita",
        subtitle = paste("Most Recent Year:", latest_year),
        fill = "kWh/person",
      ) +
      theme_minimal()

![](figs/problem%201,%20part%206-1.png) the world map illustrates how
renewable energy use per capita is distrusted globally, darker blue
regions represent higher energy use, with countries Canada and parts of
northern Europe showing the highest levels, on the other hand, many
areas in Asia and south america have some renewable energy use but at
relatively low levels

    ggplot(map_energy, aes(x = long, y = lat, group = group, fill = energy_pc)) +
      geom_polygon(color = "black", size = 0.1) +
      scale_fill_gradient(low = "lightgreen", high = "darkgreen", na.value = "grey80") +
      labs(
        title = "Primary Energy Use per Capita",
        subtitle = paste("Most Recent Year:", latest_year),
        fill = "kWh/person",
      ) +
      theme_minimal()

![](figs/problem%201,%20part%207-1.png) the graph displayed primary
energy use per person, with darker green indicating higher levels, it
shows many similarities to the previous renewable energy amp, as regions
that appeared darker before tend to appear darker here as well

    countries_to_show <- c("United States", "China", "Germany", "Brazil")

    ggplot(
      renew_gen %>% filter(Entity %in% countries_to_show),
      aes(x = Year, y = `Renewable electricity per capita`, color = Entity)
    ) +
      geom_line(size = 1.1) +
      labs(
        title = "Renewable Electricity Generation Over Time",
        x = "Year",
        y = "kWh/person"
      ) +
      theme_minimal()

![](figs/problem%201,%20part%208-1.png) this chart shows the generation
of renewable electricity over time for the following regions, Brazil,
China, Germany, and the United States. from the graph you can see that
around 1960 per person use for each of the countries was similar other
than the Uinited states use was siginificantly more, over the last 60
years, the rest have climbed and they have all been at relatively the
same level since covid

    scatter_data <- renew_latest2 %>%
      left_join(energy_latest2, by = "country")

    ggplot(scatter_data, aes(energy_pc, renew_pc)) +
      geom_point(alpha = 0.7, color = "steelblue") +
      geom_smooth(method = "lm", se = FALSE, color = "red") +
      labs(
        title = "Relationship Between Renewable Generation and Total Energy Use",
        subtitle = paste("Most Recent Year:", latest_year),
        x = "Total Energy Use",
        y = "Renewable Electricity",
      ) +
      theme_minimal()

![](figs/problem%201,%20part%209-1.png)

this graph shows the relationship between the total use of energy and
the generation of renewable energy, the red line shows the average as
the blue dots show the specific points **Problem 2**

    lyrics <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-09-29/taylor_swift_lyrics.csv")
    charts <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-09-29/charts.csv")
    sales  <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-09-29/sales.csv")

    unique(lyrics$Album)   

    ## [1] "Taylor Swift" "Fearless"     "Speak Now"    "Red"          "1989"        
    ## [6] "reputation"   "Lover"        "folklore"

    album_a <- "1989"
    album_b <- "folklore"   

    stop_words <- c("the","a","an","and","or","but","to","in","on","of","for",
                    "with","at","by","from","up","down","is","it","you","me",
                    "i","we","they","he","she","that","this","these","those")

    lyrics_clean <- lyrics %>%
      mutate(
        Lyrics = ifelse(is.na(Lyrics), "", Lyrics),
        Lyrics = as.character(Lyrics)
      )

    #tokenize
    tidy_lyrics <- lyrics_clean %>%
      separate_rows(Lyrics, sep = "\\s+") %>%
      rename(word = Lyrics) %>%
      mutate(
        word = tolower(word),
        word = str_replace_all(word, "[^a-z']", "")   
      ) %>%
      filter(word != "")   

    tidy_lyrics <- tidy_lyrics %>%
      filter(!word %in% stop_words)

    wc_a <- tidy_lyrics %>%
      filter(Album == album_a) %>%
      count(word, sort = TRUE)

    wc_b <- tidy_lyrics %>%
      filter(Album == album_b) %>%
      count(word, sort = TRUE)

    ggplot(head(wc_a, 20), aes(x = reorder(word, n), y = n)) +
      geom_col(fill = "steelblue") +
      coord_flip() +
      labs(
        title = paste("Top Words in", album_a),
        x = "Word",
        y = "Frequency"
      ) +
      theme_minimal()

![](figs/problem%202,%20part%206-1.png) The bar chart shows the most
frequently used words in taylor swifts ‘1989’ album, and the amount of
times each word was used

    ggplot(head(wc_b, 20), aes(x = reorder(word, n), y = n)) +
      geom_col(fill = "purple") +
      coord_flip() +
      labs(
        title = paste("Top Words in", album_b),
        x = "Word",
        y = "Frequency"
      ) +
      theme_minimal()

![](figs/problem%202,%20part%207-1.png) The bar chart shows the most
frequently used words in taylor swifts ‘folklore’ album, and the amount
of times each word was used

    positive_words <- c("love","happy","good","bright","smile","dream","free","sweet")
    negative_words <- c("sad","cry","bad","dark","hurt","fear","cold","alone")

    sentiment_data <- tidy_lyrics %>%
      mutate(sentiment = case_when(
        word %in% positive_words ~ "positive",
        word %in% negative_words ~ "negative",
        TRUE ~ "neutral"
      ))

    sent_compare <- sentiment_data %>%
      filter(Album %in% c(album_a, album_b)) %>%
      count(Album, sentiment)

    ggplot(sent_compare, aes(Album, n, fill = sentiment)) +
      geom_col(position = "dodge") +
      labs(
        title = paste("Sentiment Comparison:", album_a, "vs", album_b),
        x = "Album",
        y = "Word Count"
      ) +
      theme_minimal()

![](figs/problem%202,%20part%209-1.png) this bar chart shows the word
distribuition of the positive and negative words in each of the albums,
as you can see by the graph both albums have primarily neutral words.

    song_sentiment <- sentiment_data %>%
      mutate(score = case_when(
        sentiment == "positive" ~ 1,
        sentiment == "negative" ~ -1,
        TRUE ~ 0
      )) %>%
      group_by(Album, Title) %>%
      summarize(avg_sentiment = mean(score))

    charts_peak <- charts %>%
      group_by(title) %>%
      summarize(peak_position = min(chart_position, na.rm = TRUE))


    song_meta <- song_sentiment %>%
      left_join(
        charts_peak %>% rename(Title = title),   
        by = "Title"
      ) %>%
      left_join(
        sales,
        by = c("Title" = "title")
      )

    ggplot(song_meta, aes(peak_position, avg_sentiment)) +
      geom_point(color = "darkred") +
      labs(
        title = "Sentiment vs Chart Peak Position",
        x = "Peak Chart Position",
        y = "Average Sentiment"
      ) +
      theme_minimal()

![](figs/problem%202,%20part%2012-1.png) this graph shows the
distribution between the sentiment and the chart position, as you can
see from the graph the words with primarily nuetral words usually do not
hold a peak chart position, however they have before.

    ggplot(song_sentiment, aes(avg_sentiment, fill = Album)) +
      geom_histogram(bins = 20, alpha = 0.7, position = "identity") +
      labs(
        title = "Distribution of Song Sentiment by Album",
        subtitle = "Created by Ryan Zrelak",
        x = "Average Sentiment Score",
        y = "Count"
      ) +
      theme_minimal()

![](figs/problem%202,%20part%2013-1.png) this chart shows the sentiment
score vs the different albums, as you can see in this graph 1989 has a
very high average sentiment, as the other albums typically sit around
the 0 average
