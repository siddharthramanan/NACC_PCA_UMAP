# Discovering patterns in high-dimensional data with PCA and UMAP
The overlap on cognitive performance between different disorders of old age continues to remain challenging to analyse and visualise. Using three time point data from a public database (NACC) of cognitive and behavioural performance, I use PCA to derive 6 meaningful components that preserve the covariance structure of the data. I then use machine-learning non-linear decomposition methods (UMAP) to further embed this 6-dimensional PCA space to a 2D highly intuitive and visualisable UMAP space. The UMAP space showcases the graded overlap between 5 categorically different disorders.

Prior to conducting PCA, I determine the number of components underlying the dataset (at each time point) using cross-validation. This plot below shows the average number of components that underlie each time point of this dataset. The most optimal component solution is the one which has the darkest ribbon running across all iterations (lowest RMSE). The plot is produced using the following code: </br >
`df %>%`</br >
`  filter(Components %in% comps_keep) %>%`</br >
`  ggplot(aes(x=as.factor(Components), `</br >
`           y=as.factor(Iteration_no), `</br >
`           fill=CVRMSE)) +`</br >
`  facet_grid(~Timepoint) +`</br >
`  geom_raster() +`</br >
`  theme_bw() +`</br >
`  theme_classic() +`</br >
`  scale_fill_viridis() +`</br >
`  theme(axis.text= element_text(size=12), axis.title = element_text(size=12)) +`</br >
`  labs(fill='CV-RMSE value') +`</br >
`  xlab("Component number") +`</br >
`  ylab("Iteration number") +`</br >
`  theme(strip.text = element_text(size=12),`</br >
`        legend.box.background = element_rect(colour = "black"),`</br >
`        legend.background = element_blank())`</br >

![PCA_Compsel_AllTimepoints](https://user-images.githubusercontent.com/88196987/233637210-5c271345-62b7-4586-8085-6c4a7d985c84.jpeg)

A six component solution structure emerged across all time points. I extract this solution using PCA, with the loadings displayed in the following plot:
![Rplot01](https://user-images.githubusercontent.com/88196987/233637429-3324e6d9-b130-4988-94b6-5b21f1b2eeac.jpeg)

Working in a 6D multidimensional PCA space can get challenging as (i) it is hard to visualise changes across 6 mathematical dimensions; and (ii) it is difficult to capture non-linear changes across these dimensions. I therefore use UMAP to create a 2D low dimensional embedding (initialised using PCA) that allows to visualise the heterogeneity and overlap between these conditions. </br >
`umap_fit <- test_umap %>% column_to_rownames("ID.x") %>% umap(input = "data")` </br >

I extract the UMAP dimensions and merge the scores. </br >
`umap_df <- umap_fit$layout %>% as.data.frame() %>% mutate(ID.x=row_number())`

I now plot the UMAP data

![Allgroups-noconnections](https://user-images.githubusercontent.com/88196987/233639399-eb0c07da-342c-424c-9444-708e16e26946.jpeg)


  
