# Air Quality Downscaling Attempt — Barcelona Region

Inspired by the BSC research opening, I am attempting to make a PoC for downscaling AQ using Supervised ML. 

## What I am trying to do
I am using coarse models CAMS reanalysis data, which estimates at almost a 80km resolution, and attempting to downscale it to much finer resolution using Air Quality Monitoring Stations (AQMS) data as ground truth at several points within Barcelona.

So far, my data sources are: 
CAMS Global Reanalysis (EAC4) — PM2.5, daily, 0.75° resolution, 2022
Catalan Air Quality Network — Ground station PM2.5 observations, Barcelona, 2022
I am using 2022 because it post-lockdown period when things were already reverted back to the normal. This would be more representative of the reality. Then data from 2023, 2024 and onwards can be used to further validate the trained models.

## Work done so far
- CAMS data acquisition, NetCDF format. (xarray)
- CAMS data visualization (cartopy)
- AQMS data acquisition via API, csv format.
- AQMS data wrangling (pandas) 
- AQMS and CAMS data merge
- Baseline Linear Regression model
- Feature engineering with experiment tracking

### Baseline results with Linear Regression
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>features</th>
      <th>r2</th>
      <th>mae</th>
      <th>rmse</th>
    </tr>
    <tr>
      <th>run</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>baseline_cams_only</th>
      <td>['pm25_cams']</td>
      <td>0.094</td>
      <td>4.212</td>
      <td>6.340</td>
    </tr>
    <tr>
      <th>baseline_cams_month</th>
      <td>['pm25_cams', 'month']</td>
      <td>0.040</td>
      <td>4.333</td>
      <td>6.526</td>
    </tr>
    <tr>
      <th>baseline_cams_month_seasons</th>
      <td>['pm25_cams', 'month', 'season_autumn', 'seaso...</td>
      <td>0.063</td>
      <td>4.467</td>
      <td>6.448</td>
    </tr>
  </tbody>
</table>
</div>


## Next Steps
- Random Forest, XGBoost over the same features
- Expand to more AQMS in Catalonia
- Add terrain features
- Use deep learning (can try CNN, OR statistical Kriging, or Gaussian Process Regression)

