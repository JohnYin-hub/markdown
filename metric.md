### metrics

```python
def metrics(y_true, y_pred):
    print(
        "precision: {} \n recall: {} \n f1: {}".format(
            precision_score(y_true, y_pred),
            recall_score(y_true, y_pred),
            f1_score(y_true, y_pred)
        )
    )
    
    
def my_metrics(y_true, y_pred):
    """
    precision,recall,fpr,f1
    """
    tp,tn,fp,fn = 0,0,0,0
    for t,p in zip(y_true, y_pred):
        if t == 1 and p == 1:
            tp += 1
        elif t == 1 and p == 0:
            fn += 1
        elif t == 0 and p == 1:
            fp += 1
        elif t == 0 and p == 0:
            tn += 1
    precision = tp / (tp+fp+ 0.000001)
    recall = tp / (tp+fn+ 0.000001)
    fpr = fp / (tn + fp + 0.000001)
    f1 = 2*precision*recall / (precision+recall)
    print("precision: {:20} \n recall: {:20} \n f1: {:20} \n fpr: {:20} ".format(precision,recall,f1,fpr))
    return precision,recall,f1,fpr
```

