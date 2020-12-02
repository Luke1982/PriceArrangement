# PriceArrangement
A hard fork of the DiscountLine module

This module was forked because the [original](https://github.com/tsolucio/PriceCalculation) module does not feel logical to me. I will explain the changes in respect to the original below

## Order of precedense
When the pricefilter on a product or service is performed, this version will look for discount lines in the following order and stop looking when it finds one. The word 'cliënt' is interchangeable for either an Account or Contact.

1. Cliënt and product are directly linked (through the related lists on a PriceArrangement record) and the PriceArrangement category is '--None--' (or your local translation of '--None--')
2. No cliënt or product is linked to the PriceArrangement record but there is a PriceArrangement record where the category matches that of the product or service
3. The PriceArrangement category is set to '--None--', there is no matching product or service found but there is a cliënt found. This PriceArrangement record should have no product or service linked, so that it can be used to set a discount for an entire cliënt.
4. The PriceArrangement category is set to '--None--', there is no matching cliënt found but there is a product or service found.

**IMPORTANT**
Read the above again, since it is bound to cause confusion. When the price for a product or service is requested to the system, the PriceArrangement module will take **all the above** steps. Meaning: if it can't find a result for number 1, it'll try number 2, and so on. So if you want to make sure a product or service gets _NO_ discount, make sure your particular use case is not covered in any of these conditions.

## After installation
- Don't forget to activate the module