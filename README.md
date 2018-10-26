## Predicting Label Costs with Regression

1. The Problem
2. The Dataset
3. The Models
4. Conclusion

**1. Motivation**

Company X makes product identification labels for manufacturing businesses that improves their ability to identify, track, and market their products. Since labels have to meet needs of different manufacturers and comply with industry-specific product identification regulations, they have to be produced in a variety of shapes, can be made in several sizes, using different papers, inks, adhesives, etc. The goal was to identify which of these product features drive production costs and find a predictive model to improve pricing strategy. 

**2. The Dataset**
The dataset contains 222,904 entries and 18 columns. The data was significantly transformed for modeling.

* MEASUREMENTS: all measurements were converted onto a common scale (millimeter). Since measurements are defined by SHAPE (for example, a circle has a diameter but no length or width) all missing values in LENGTH, WIDTH, DIAMETER, and VERTICAL_GAP were filled with zero. Diameters over 10mm were dropped as errors. Unusually high values for LENGTH, WIDTH, and VERTICAL_GAP were left in the dataset and may result in worse predictions. The same is true for unusually high values in NO_ACROSS.
* DUPLICATES: MATERIAL_DESCRIPTION and ITEM_DESCRIPTION columns were dropped as they contain information contained in other columns.
* SALES OUTLIERS: dropped zero and minus amounts in sales, costs and price. Unusually high values were left in the dataset and may result in worse predictions.
* DATES: the INVOICE_DATE column was transformed into new features (year, month, day, day of the week).
* MISSING VALUES: dropped missing values in ITEM (470 values), SHAPE (440), and NO_ACROSS (440).
* MATERIAL_NO: dropped ‘NC’ (‘not configured’) and ‘PURCHASED’ observations (232 values)

**3. The Models**

The following algorithms were used for modeling:
* stochastic gradient descent, lasso and ridge regressions for exploring linear relationships between predictive features and cost;
* random forest for exploring non-linear relationships.

Here's a great animation from a blogpost by George Seif that shows how random forest works: 
![2014-10-22 11_35_09](https://cdn-images-1.medium.com/max/1760/1*9kACduxnce_JdTrftM_bsA.gif)

**4. Conclusion**

Random forest outperformed regularized regression by a large margin, producing an R-squared so high that the model is likely overfitting despite using five-fold cross-validation, setting aside a test set, and not letting the trees grow deep. New data was requested to see if random forest would continue to perform well. In the meantime, in order to create a tool that can be easily adopted across the sales organization, regularized regression based solution is under development.

