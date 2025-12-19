# The calculation of the confidence interval
The function `confidence_interval` is used for calculating the confidence interval of a paramter fixed by fitting within $68\%$, $95\%$ confidence levels.

```julia
function confidence_interval(data::Vector{Float64}; k=1.5, cl=68e-2)
    filter_data = IQR_outlier_detection(data, k=k)
    # mean = Statistics.mean(filter_data)
    std = Statistics.std(filter_data)
    # cl : z
    # 0.68: 1 
    # 0.95:  1.96
    alpha = 1. - cl
    z = Statistics.quantile(Distributions.Normal(), 1- alpha/2)
    # Calculate margin of error
    merr = z * std
    return merr
end
```
