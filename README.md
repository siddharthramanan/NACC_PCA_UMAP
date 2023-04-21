# NACC_PCA_UMAP
NACC PCA UMAP project (for display on portfolio)




I first use cross-validation (10 iterations) to select the number of components that underlie this dataset. This plot below shows the average number of components that underlie each time point of this dataset. The plot is produced using the following code:
`nacc_voi_dem_all_rmsecvCompsel_2 %>%`</br >
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
