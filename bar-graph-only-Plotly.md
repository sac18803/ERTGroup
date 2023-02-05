---
title: "Untitled"
author: "Darrin Thomas"
date: '2023-02-05'
output: 
  html_document:
    keep_md: true
---
This demonstration will show you how to make interactive bar graphs using Plotly. Below we load all of the needed libraries.



Plotly is the library for makint the graphs. Ecdat is were the data will come from. dplyr and forcats are used for data manipulation.

In the code below we are going to make a table from which we will derive are bar graphs. The data we are using is the PSID dataset which provides some information on such variables as marital status, education, age, and other data.


```r
#bar graphs
married_table <- PSID %>%
        count(married)

married_table
```

```
##         married    n
## 1       married 3071
## 2 never married  681
## 3       widowed   90
## 4      divorced  645
## 5     separated  317
## 6         NA/DF    9
## 7  no histories   43
```

Next, we will make are first bar graph. It is a simple graph that shows the marital status of the respondents.


```r
# Create a bar chart of marriage
married_table %>%
        plot_ly(x=~married, y= ~n) %>%
        add_bars()
```

```{=html}
<div class="plotly html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-a1f95ac8164340982df1" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-a1f95ac8164340982df1">{"x":{"visdat":{"5bc07b859433":["function () ","plotlyVisDat"]},"cur_data":"5bc07b859433","attrs":{"5bc07b859433":{"x":{},"y":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"bar","inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"xaxis":{"domain":[0,1],"automargin":true,"title":"married","type":"category","categoryorder":"array","categoryarray":["married","never married","widowed","divorced","separated","NA/DF","no histories"]},"yaxis":{"domain":[0,1],"automargin":true,"title":"n"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"x":["married","never married","widowed","divorced","separated","NA/DF","no histories"],"y":[3071,681,90,645,317,9,43],"type":"bar","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"error_y":{"color":"rgba(31,119,180,1)"},"error_x":{"color":"rgba(31,119,180,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

In the graph below, we will rearrange the order of the bars so they are shown for largest to smallest. This is often much more visually appealing for the audience. To do this we will use the fct_reorder function from the forcats library. Below is the code and the output.


```r
## Reorder bars
married_table %>%
        mutate(married = fct_reorder(married, 
                                     n, .desc = T)) %>% #fct_reorder from forcats
        plot_ly(x = ~married, y = ~n) %>% 
        add_bars() 
```

```{=html}
<div class="plotly html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-bef04b3abb58d2e5ae5b" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-bef04b3abb58d2e5ae5b">{"x":{"visdat":{"5bc07167836f":["function () ","plotlyVisDat"]},"cur_data":"5bc07167836f","attrs":{"5bc07167836f":{"x":{},"y":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"bar","inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"xaxis":{"domain":[0,1],"automargin":true,"title":"married","type":"category","categoryorder":"array","categoryarray":["married","never married","divorced","separated","widowed","no histories","NA/DF"]},"yaxis":{"domain":[0,1],"automargin":true,"title":"n"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"x":["married","never married","widowed","divorced","separated","NA/DF","no histories"],"y":[3071,681,90,645,317,9,43],"type":"bar","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"error_y":{"color":"rgba(31,119,180,1)"},"error_x":{"color":"rgba(31,119,180,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

The code below is mostly the same. The only difference is that we are adding a label for the x and y axis. This is done by adding the layout function and including the needed information. 


```r
#Add axes titles
married_table %>%
        mutate(married = fct_reorder(married, 
                                     n, .desc = T)) %>% #fct_reorder from forcats
        plot_ly(x = ~married, y = ~n) %>% 
        add_bars() %>% 
        layout(xaxis = list(title= "Marital Status",
                            showgrid=T),
               yaxis = list(title="Count"))
```

```{=html}
<div class="plotly html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-3c5b5aedff35b28a44c0" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-3c5b5aedff35b28a44c0">{"x":{"visdat":{"5bc073aa998b":["function () ","plotlyVisDat"]},"cur_data":"5bc073aa998b","attrs":{"5bc073aa998b":{"x":{},"y":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"bar","inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"xaxis":{"domain":[0,1],"automargin":true,"title":"Marital Status","showgrid":true,"type":"category","categoryorder":"array","categoryarray":["married","never married","divorced","separated","widowed","no histories","NA/DF"]},"yaxis":{"domain":[0,1],"automargin":true,"title":"Count"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"x":["married","never married","widowed","divorced","separated","NA/DF","no histories"],"y":[3071,681,90,645,317,9,43],"type":"bar","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"error_y":{"color":"rgba(31,119,180,1)"},"error_x":{"color":"rgba(31,119,180,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

The code below shows how to create hover info. What this means is that when the most hovers over a bar in the bar graph it will display information that we want. To do this you have to add the hoverinfo argument to the plot_ly function as shown below.


```r
#hoverinfo
PSID %>%
        count(married) %>%
        plot_ly(x=~married, y=~n, hoverinfo="y") %>%
        add_bars()
```

```{=html}
<div class="plotly html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-4c14492e4b0fc74059be" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-4c14492e4b0fc74059be">{"x":{"visdat":{"5bc06a2fed8e":["function () ","plotlyVisDat"]},"cur_data":"5bc06a2fed8e","attrs":{"5bc06a2fed8e":{"x":{},"y":{},"hoverinfo":"y","alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"bar","inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"xaxis":{"domain":[0,1],"automargin":true,"title":"married","type":"category","categoryorder":"array","categoryarray":["married","never married","widowed","divorced","separated","NA/DF","no histories"]},"yaxis":{"domain":[0,1],"automargin":true,"title":"n"},"hovermode":"closest","showlegend":false},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"x":["married","never married","widowed","divorced","separated","NA/DF","no histories"],"y":[3071,681,90,645,317,9,43],"hoverinfo":["y","y","y","y","y","y","y"],"type":"bar","marker":{"color":"rgba(31,119,180,1)","line":{"color":"rgba(31,119,180,1)"}},"error_y":{"color":"rgba(31,119,180,1)"},"error_x":{"color":"rgba(31,119,180,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

  THe final shows ow to make stacked bar graph. By stacking the bars we are able to include an additional variable in the graph. For our purpose we will display a count of sex and major together. To this you must specify the color in the plot_ly function and the type of barmode in the layout function.
  

```r
#stackbar
Mathlevel %>%
        count(sex, major) %>%
        plot_ly(x = ~sex, y = ~n, color = ~major) %>%
        add_bars() %>%
        layout(barmode = 'stack')
```

```{=html}
<div class="plotly html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-b7c444e0cb6017fec26c" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-b7c444e0cb6017fec26c">{"x":{"visdat":{"5bc057c4847c":["function () ","plotlyVisDat"]},"cur_data":"5bc057c4847c","attrs":{"5bc057c4847c":{"x":{},"y":{},"color":{},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"bar","inherit":true}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"barmode":"stack","xaxis":{"domain":[0,1],"automargin":true,"title":"sex","type":"category","categoryorder":"array","categoryarray":["male","female"]},"yaxis":{"domain":[0,1],"automargin":true,"title":"n"},"hovermode":"closest","showlegend":true},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"x":["male","female"],"y":[79,51],"type":"bar","name":"other","marker":{"color":"rgba(102,194,165,1)","line":{"color":"rgba(102,194,165,1)"}},"textfont":{"color":"rgba(102,194,165,1)"},"error_y":{"color":"rgba(102,194,165,1)"},"error_x":{"color":"rgba(102,194,165,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":["male","female"],"y":[144,65],"type":"bar","name":"eco","marker":{"color":"rgba(252,141,98,1)","line":{"color":"rgba(252,141,98,1)"}},"textfont":{"color":"rgba(252,141,98,1)"},"error_y":{"color":"rgba(252,141,98,1)"},"error_x":{"color":"rgba(252,141,98,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":["male","female"],"y":[55,48],"type":"bar","name":"oss","marker":{"color":"rgba(141,160,203,1)","line":{"color":"rgba(141,160,203,1)"}},"textfont":{"color":"rgba(141,160,203,1)"},"error_y":{"color":"rgba(141,160,203,1)"},"error_x":{"color":"rgba(141,160,203,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":["male","female"],"y":[71,55],"type":"bar","name":"ns","marker":{"color":"rgba(231,138,195,1)","line":{"color":"rgba(231,138,195,1)"}},"textfont":{"color":"rgba(231,138,195,1)"},"error_y":{"color":"rgba(231,138,195,1)"},"error_x":{"color":"rgba(231,138,195,1)"},"xaxis":"x","yaxis":"y","frame":null},{"x":["male","female"],"y":[24,17],"type":"bar","name":"hum","marker":{"color":"rgba(166,216,84,1)","line":{"color":"rgba(166,216,84,1)"}},"textfont":{"color":"rgba(166,216,84,1)"},"error_y":{"color":"rgba(166,216,84,1)"},"error_x":{"color":"rgba(166,216,84,1)"},"xaxis":"x","yaxis":"y","frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

