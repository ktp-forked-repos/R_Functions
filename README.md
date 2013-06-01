R_Functions
===========

###1. `trimdata()` 

  `trimdata(dataset, dv, factors = NULL, tr = 3, rm = FALSE, min.val = NULL, max.val = NULL)` 

This function trims numerical data based on different factors. 

* `dataset`: the name of the dataset, in the form of data frame, in which data are stored.
  
* `dv`: the name of the variable to be trimmed.
  
* `factors`: the factors on which trimming is based. For example, if a user specifies two 2-level factors, there will be a total of 4 conditions. The mean and the standard deviation of each condition will be computed to calculate trimming criteria. When `factors=NULL`, trimming is done to the entire dataset at once.
  
* `tr`: number of standard deviations used to set the trimming criteria - that is, data points that are `+/- tr*SD` away from the mean are considered outliers. By default, `3SD` is used; in other words, data points that are 3 standard deviations away from the mean of a condition (or of the entire data set if `factors=NULL`) are declared as outliers.
* `rm`: whether outliers are removed or replaced. By default, `rm=FALSE` - that is, if a data point is declared as an outlier, it will be replaced by `mean + tr*SD` or `mean - tr*SD` - dependent on whether the outlier lies outside the upper bound or lower bound. If the argument is set to TRUE, outliers will be replaced by `NA`.
* `min.val`|`max.val`: whether any extreme values are to be removed before applying the standard deviation based trimming procedure. Inflation of standard deviation can be reduced this way. By default, both arguments are set to `NULL`. Any extreme values to be removed will be replaced by `NA`.

The function will return an invisible vector of values of the same length as the original variable, which can be saved into an R object or appended to the original data frame.
  
  Example: 

    data(ChickWeight)
    (trimdata(ChickWeight, dv=weight, factors=c(Time, Diet), tr=2, rm=TRUE))
    #24 data points (4.15%) have been removed.
    #output
    # [1]  42  51  59  64  76  93 106 125 149 171 199 205  40  49  58  72  84 103 122 138 162 187 209 215  43)
    # [26]  39  55  67  84  99 115 138 163 187 198 202  42  49  56  67  74  87 102 108 136 154 160 157  41  42
    # [51]  NA  60  79 106 141 164 197 199 220 223  41  49  59  74  97 124 141 148 155 160 160 157  41  49  57
    # [76]  71  89 112 146 174 218 250  NA  NA  42  50  61  71  84  93 110 116 126 134 125  42  51  59  68  85
    #[101]  96  90  92  93 100 100  98  41  44  52  63  74  81  89  96 101 112 120 124  43  51  63  NA  NA  NA
    #[126] 168 177 182 184 181 175  41  49  56  62  72  88 119 135 162 185 195 205  41  48  53  60  65  67  71
    #[151]  70  71  81  91  96  41  49  62  79 101 128 164 192 227 248 259 266  41  49  56  64  68  68  67  68
    #[176]  41  45  49  NA  57  51  54  42  51  61  72  83  89  98 103 113 123 133 142  NA  NA  43  48  55  62
    #[201]  65  71  82  88 106 120 144 157  41  47  54  58  65  73  77  89  98 107 115 117  40  50  62  NA  NA
    #[226]  NA  NA  NA  NA 307 318 331  41  55  64  77  90  95 108 111 131 148 164 167  43  52  61  73  90 103
    #[251] 127 135 145 163 170 175  42  52  58  74  66  68  70  71  72  72  76  74  40  49  62  78 102 124 146
    #[276] 164 197 231 259 265  42  48  57  74  93 114 136 147 169 205 236 251  39  46  58  73  87 100 115 123
    #[301] 144 163 185 192  39  46  58  73  92 114 145 156 184 207 212 233  39  48  59  74  87 106 134 150 187
    #[326] 230 279 309  42  48  59  72  85  98 115 122 143 151 157 150  42  53  62  73  85 102 123 138 170 204
    #[351] 235 256  41  49  65  82 107 129 159 179 221 263 291 305  39  50  63  77  96 111 137 144 151 146 156
    #[376] 147  41  49  63  85 107 134 164 186 235 294 327 341  41  53  64  87 123  NA  NA  NA  NA 332 361 373
    #[401]  39  48  61  76  98 116 145 166 198 227 225 220  41  48  NA  68  80  83 103 112 135 157 169 178  41
    #[426]  49  61  74  98 109 128 154 192 232 280 290  42  50  61  78  89 109 130 146 170 214 250 272  41  55
    #[451]  66  79 101 120 154 182 215 262 295 321  42  51  66  85 103 124 155 153 175 184 199 204  42  49  63
    #[476]  84 103 126 160 174 204 234 269 281  42  55  69  NA  NA  NA  NA 188 197 198 199 200  42  51  65  86
    #[501] 103 118 127 138 145 146  41  50  61  78  98 117 135 141 147 174 197 196  40  52  62  82 101 120 144
    #[526] 156 173 210 231 238  41  53  66  79 100 123 148 157 168 185 210 205  39  50  62  80 104 125 154 170
    #[551] 222 261 303 322  40  53  64  85 108 128 152 166 184 203 233 237  41  54  67  84 105 122 155 175 205
    #[576] 234 264 264
