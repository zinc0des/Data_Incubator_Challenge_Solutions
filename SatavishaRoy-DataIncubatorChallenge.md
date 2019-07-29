
## Q1. For all citations, what is the mean violation fine?


```python
import pandas as pd
import numpy as np
import matplotlib
import matplotlib.pyplot as plt
%matplotlib inline  
```


```python
citation = pd.read_csv('./Parking_Citations.csv')
cite2 = citation.copy()
cite2.head()
```

    /Users/satavisha/anaconda3/envs/py3env/lib/python3.7/site-packages/IPython/core/interactiveshell.py:3057: DtypeWarning: Columns (2,17,18,20) have mixed types. Specify dtype option on import or set low_memory=False.
      interactivity=interactivity, compiler=compiler, result=result)





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Citation</th>
      <th>Tag</th>
      <th>ExpMM</th>
      <th>ExpYY</th>
      <th>State</th>
      <th>Make</th>
      <th>Address</th>
      <th>ViolCode</th>
      <th>Description</th>
      <th>ViolFine</th>
      <th>...</th>
      <th>Balance</th>
      <th>PenaltyDate</th>
      <th>OpenFine</th>
      <th>OpenPenalty</th>
      <th>NoticeDate</th>
      <th>ImportDate</th>
      <th>Neighborhood</th>
      <th>PoliceDistrict</th>
      <th>CouncilDistrict</th>
      <th>Location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>82691651</td>
      <td>69943CF</td>
      <td>04</td>
      <td>19.0</td>
      <td>MD</td>
      <td>MAZD</td>
      <td>1300 BLK EAST NORTHERN PKWY WB</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/26/2018 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1300 BLK EAST NORTHERN PKWY\nWB Baltimore, MD\...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>85937226</td>
      <td>T720887</td>
      <td>12</td>
      <td>18.0</td>
      <td>MD</td>
      <td>ACUR</td>
      <td>300 BLK NORTH BEND RD SB</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>40.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>01/03/2019 04:33:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>82691115</td>
      <td>5BA2678</td>
      <td>03</td>
      <td>19.0</td>
      <td>MD</td>
      <td>TOYT</td>
      <td>5000 BLK ROLAND AVE NB</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/26/2018 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5000 BLK ROLAND AVE\nNB Baltimore, MD\n(39.353...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>82694689</td>
      <td>5BT8544</td>
      <td>01</td>
      <td>18.0</td>
      <td>MD</td>
      <td>FORD</td>
      <td>2400 BLK ERDMAN AVE NB</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/26/2018 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2400 BLK ERDMAN AVE\nNB Baltimore, MD\n(39.325...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>82691214</td>
      <td>1BV0537</td>
      <td>11</td>
      <td>18.0</td>
      <td>MD</td>
      <td>SUBA</td>
      <td>1300 BLK WEST COLD SPRING LN W</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/26/2018 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1300 BLK WEST COLD SPRING LN W\nBaltimore, MD\...</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>




```python
cite2.shape
```




    (3385279, 21)




```python
dir(cite2)
```




    ['Address',
     'Balance',
     'Citation',
     'CouncilDistrict',
     'Description',
     'ExpMM',
     'ExpYY',
     'ImportDate',
     'Location',
     'Make',
     'Neighborhood',
     'NoticeDate',
     'OpenFine',
     'OpenPenalty',
     'PenaltyDate',
     'PoliceDistrict',
     'State',
     'T',
     'Tag',
     'ViolCode',
     'ViolDate',
     'ViolFine',
     '_AXIS_ALIASES',
     '_AXIS_IALIASES',
     '_AXIS_LEN',
     '_AXIS_NAMES',
     '_AXIS_NUMBERS',
     '_AXIS_ORDERS',
     '_AXIS_REVERSED',
     '__abs__',
     '__add__',
     '__and__',
     '__array__',
     '__array_priority__',
     '__array_wrap__',
     '__bool__',
     '__class__',
     '__contains__',
     '__copy__',
     '__deepcopy__',
     '__delattr__',
     '__delitem__',
     '__dict__',
     '__dir__',
     '__div__',
     '__doc__',
     '__eq__',
     '__finalize__',
     '__floordiv__',
     '__format__',
     '__ge__',
     '__getattr__',
     '__getattribute__',
     '__getitem__',
     '__getstate__',
     '__gt__',
     '__hash__',
     '__iadd__',
     '__iand__',
     '__ifloordiv__',
     '__imod__',
     '__imul__',
     '__init__',
     '__init_subclass__',
     '__invert__',
     '__ior__',
     '__ipow__',
     '__isub__',
     '__iter__',
     '__itruediv__',
     '__ixor__',
     '__le__',
     '__len__',
     '__lt__',
     '__matmul__',
     '__mod__',
     '__module__',
     '__mul__',
     '__ne__',
     '__neg__',
     '__new__',
     '__nonzero__',
     '__or__',
     '__pos__',
     '__pow__',
     '__radd__',
     '__rand__',
     '__rdiv__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__rfloordiv__',
     '__rmatmul__',
     '__rmod__',
     '__rmul__',
     '__ror__',
     '__round__',
     '__rpow__',
     '__rsub__',
     '__rtruediv__',
     '__rxor__',
     '__setattr__',
     '__setitem__',
     '__setstate__',
     '__sizeof__',
     '__str__',
     '__sub__',
     '__subclasshook__',
     '__truediv__',
     '__weakref__',
     '__xor__',
     '_accessors',
     '_add_numeric_operations',
     '_add_series_only_operations',
     '_add_series_or_dataframe_operations',
     '_agg_by_level',
     '_agg_examples_doc',
     '_agg_summary_and_see_also_doc',
     '_aggregate',
     '_aggregate_multiple_funcs',
     '_align_frame',
     '_align_series',
     '_box_col_values',
     '_box_item_values',
     '_builtin_table',
     '_check_inplace_setting',
     '_check_is_chained_assignment_possible',
     '_check_label_or_level_ambiguity',
     '_check_percentile',
     '_check_setitem_copy',
     '_clear_item_cache',
     '_clip_with_one_bound',
     '_clip_with_scalar',
     '_combine_const',
     '_combine_frame',
     '_combine_match_columns',
     '_combine_match_index',
     '_consolidate',
     '_consolidate_inplace',
     '_construct_axes_dict',
     '_construct_axes_dict_from',
     '_construct_axes_from_arguments',
     '_constructor',
     '_constructor_expanddim',
     '_constructor_sliced',
     '_convert',
     '_count_level',
     '_create_indexer',
     '_cython_table',
     '_data',
     '_deprecations',
     '_dir_additions',
     '_dir_deletions',
     '_drop_axis',
     '_drop_labels_or_levels',
     '_ensure_valid_index',
     '_find_valid_index',
     '_from_arrays',
     '_from_axes',
     '_get_agg_axis',
     '_get_axis',
     '_get_axis_name',
     '_get_axis_number',
     '_get_axis_resolvers',
     '_get_block_manager_axis',
     '_get_bool_data',
     '_get_cacher',
     '_get_index_resolvers',
     '_get_item_cache',
     '_get_label_or_level_values',
     '_get_numeric_data',
     '_get_space_character_free_column_resolvers',
     '_get_value',
     '_get_values',
     '_getitem_bool_array',
     '_getitem_frame',
     '_getitem_multilevel',
     '_gotitem',
     '_iget_item_cache',
     '_indexed_same',
     '_info_axis',
     '_info_axis_name',
     '_info_axis_number',
     '_info_repr',
     '_init_mgr',
     '_internal_get_values',
     '_internal_names',
     '_internal_names_set',
     '_is_builtin_func',
     '_is_cached',
     '_is_copy',
     '_is_cython_func',
     '_is_datelike_mixed_type',
     '_is_homogeneous_type',
     '_is_label_or_level_reference',
     '_is_label_reference',
     '_is_level_reference',
     '_is_mixed_type',
     '_is_numeric_mixed_type',
     '_is_view',
     '_ix',
     '_ixs',
     '_join_compat',
     '_maybe_cache_changed',
     '_maybe_update_cacher',
     '_metadata',
     '_needs_reindex_multi',
     '_obj_with_exclusions',
     '_protect_consolidate',
     '_reduce',
     '_reindex_axes',
     '_reindex_columns',
     '_reindex_index',
     '_reindex_multi',
     '_reindex_with_indexers',
     '_repr_data_resource_',
     '_repr_fits_horizontal_',
     '_repr_fits_vertical_',
     '_repr_html_',
     '_repr_latex_',
     '_reset_cache',
     '_reset_cacher',
     '_sanitize_column',
     '_selected_obj',
     '_selection',
     '_selection_list',
     '_selection_name',
     '_series',
     '_set_as_cached',
     '_set_axis',
     '_set_axis_name',
     '_set_is_copy',
     '_set_item',
     '_set_value',
     '_setitem_array',
     '_setitem_frame',
     '_setitem_slice',
     '_setup_axes',
     '_shallow_copy',
     '_slice',
     '_stat_axis',
     '_stat_axis_name',
     '_stat_axis_number',
     '_to_dict_of_blocks',
     '_try_aggregate_string_function',
     '_typ',
     '_unpickle_frame_compat',
     '_unpickle_matrix_compat',
     '_update_inplace',
     '_validate_dtype',
     '_values',
     '_where',
     '_xs',
     'abs',
     'add',
     'add_prefix',
     'add_suffix',
     'agg',
     'aggregate',
     'align',
     'all',
     'any',
     'append',
     'apply',
     'applymap',
     'as_matrix',
     'asfreq',
     'asof',
     'assign',
     'astype',
     'at',
     'at_time',
     'axes',
     'between_time',
     'bfill',
     'bool',
     'boxplot',
     'clip',
     'clip_lower',
     'clip_upper',
     'columns',
     'combine',
     'combine_first',
     'compound',
     'copy',
     'corr',
     'corrwith',
     'count',
     'cov',
     'cummax',
     'cummin',
     'cumprod',
     'cumsum',
     'describe',
     'diff',
     'div',
     'divide',
     'dot',
     'drop',
     'drop_duplicates',
     'droplevel',
     'dropna',
     'dtypes',
     'duplicated',
     'empty',
     'eq',
     'equals',
     'eval',
     'ewm',
     'expanding',
     'explode',
     'ffill',
     'fillna',
     'filter',
     'first',
     'first_valid_index',
     'floordiv',
     'from_dict',
     'from_records',
     'ftypes',
     'ge',
     'get',
     'get_dtype_counts',
     'get_ftype_counts',
     'get_values',
     'groupby',
     'gt',
     'head',
     'hist',
     'iat',
     'idxmax',
     'idxmin',
     'iloc',
     'index',
     'infer_objects',
     'info',
     'insert',
     'interpolate',
     'isin',
     'isna',
     'isnull',
     'items',
     'iteritems',
     'iterrows',
     'itertuples',
     'ix',
     'join',
     'keys',
     'kurt',
     'kurtosis',
     'last',
     'last_valid_index',
     'le',
     'loc',
     'lookup',
     'lt',
     'mad',
     'mask',
     'max',
     'mean',
     'median',
     'melt',
     'memory_usage',
     'merge',
     'min',
     'mod',
     'mode',
     'mul',
     'multiply',
     'ndim',
     'ne',
     'nlargest',
     'notna',
     'notnull',
     'nsmallest',
     'nunique',
     'pct_change',
     'pipe',
     'pivot',
     'pivot_table',
     'plot',
     'pop',
     'pow',
     'prod',
     'product',
     'quantile',
     'query',
     'radd',
     'rank',
     'rdiv',
     'reindex',
     'reindex_like',
     'rename',
     'rename_axis',
     'reorder_levels',
     'replace',
     'resample',
     'reset_index',
     'rfloordiv',
     'rmod',
     'rmul',
     'rolling',
     'round',
     'rpow',
     'rsub',
     'rtruediv',
     'sample',
     'select_dtypes',
     'sem',
     'set_axis',
     'set_index',
     'shape',
     'shift',
     'size',
     'skew',
     'slice_shift',
     'sort_index',
     'sort_values',
     'sparse',
     'squeeze',
     'stack',
     'std',
     'style',
     'sub',
     'subtract',
     'sum',
     'swapaxes',
     'swaplevel',
     'tail',
     'take',
     'to_clipboard',
     'to_csv',
     'to_dense',
     'to_dict',
     'to_excel',
     'to_feather',
     'to_gbq',
     'to_hdf',
     'to_html',
     'to_json',
     'to_latex',
     'to_msgpack',
     'to_numpy',
     'to_parquet',
     'to_period',
     'to_pickle',
     'to_records',
     'to_sparse',
     'to_sql',
     'to_stata',
     'to_string',
     'to_timestamp',
     'to_xarray',
     'transform',
     'transpose',
     'truediv',
     'truncate',
     'tshift',
     'tz_convert',
     'tz_localize',
     'unstack',
     'update',
     'values',
     'var',
     'where',
     'xs']




```python
#citation.describe
```


```python
cite2.columns
```




    Index(['Citation', 'Tag', 'ExpMM', 'ExpYY', 'State', 'Make', 'Address',
           'ViolCode', 'Description', 'ViolFine', 'ViolDate', 'Balance',
           'PenaltyDate', 'OpenFine', 'OpenPenalty', 'NoticeDate', 'ImportDate',
           'Neighborhood', 'PoliceDistrict', 'CouncilDistrict', 'Location'],
          dtype='object')




```python
cite2.dtypes
```




    Citation             int64
    Tag                 object
    ExpMM               object
    ExpYY              float64
    State               object
    Make                object
    Address             object
    ViolCode             int64
    Description         object
    ViolFine           float64
    ViolDate            object
    Balance            float64
    PenaltyDate        float64
    OpenFine           float64
    OpenPenalty        float64
    NoticeDate          object
    ImportDate          object
    Neighborhood        object
    PoliceDistrict      object
    CouncilDistrict    float64
    Location            object
    dtype: object




```python
cite2.loc[:, 'ViolFine'].mean()
```




    49.897334015896476



## Looking only at vehicles that have open penalty fees, what dollar amount is the 81st percentile of that group?


```python
op_over_0 = cite2[cite2.OpenPenalty > 0.0]
```


```python
op_over_0['OpenPenalty'].quantile(0.81)
```




    480.0



## Find all citations where the police district has been given. Next, determine which district has the highest mean violation fine. What is that mean violation fine? Keep in mind that Baltimore is divided into nine police districts, so clean the data accordingly.


```python
pol_dis = cite2[cite2['PoliceDistrict'].notna()]
pol_dis
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Citation</th>
      <th>Tag</th>
      <th>ExpMM</th>
      <th>ExpYY</th>
      <th>State</th>
      <th>Make</th>
      <th>Address</th>
      <th>ViolCode</th>
      <th>Description</th>
      <th>ViolFine</th>
      <th>...</th>
      <th>Balance</th>
      <th>PenaltyDate</th>
      <th>OpenFine</th>
      <th>OpenPenalty</th>
      <th>NoticeDate</th>
      <th>ImportDate</th>
      <th>Neighborhood</th>
      <th>PoliceDistrict</th>
      <th>CouncilDistrict</th>
      <th>Location</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>434</th>
      <td>31807</td>
      <td>9AE0437</td>
      <td>08</td>
      <td>12.0</td>
      <td>MD</td>
      <td>HOND</td>
      <td>600 AISQUITH ST</td>
      <td>18</td>
      <td>All Other Parking Meter Violations</td>
      <td>32.0</td>
      <td>...</td>
      <td>357.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>300.0</td>
      <td>09/18/2012</td>
      <td>04/09/2014 04:01:00 AM</td>
      <td>Oldtown</td>
      <td>Eastern</td>
      <td>12.0</td>
      <td>600 AISQUITH ST\nBaltimore, MD</td>
    </tr>
    <tr>
      <th>435</th>
      <td>31815</td>
      <td>3AS5633</td>
      <td>06</td>
      <td>12.0</td>
      <td>MD</td>
      <td>FORD</td>
      <td>600 AISQUITH ST</td>
      <td>18</td>
      <td>All Other Parking Meter Violations</td>
      <td>32.0</td>
      <td>...</td>
      <td>332.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>300.0</td>
      <td>09/26/2012</td>
      <td>04/09/2014 04:01:00 AM</td>
      <td>Oldtown</td>
      <td>Eastern</td>
      <td>12.0</td>
      <td>600 AISQUITH ST\nBaltimore, MD</td>
    </tr>
    <tr>
      <th>519</th>
      <td>5044608</td>
      <td>7DC3668</td>
      <td>01</td>
      <td>18.0</td>
      <td>MD</td>
      <td>NISS</td>
      <td>509 N GILMOR ST</td>
      <td>22</td>
      <td>Expired Tags</td>
      <td>32.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>05/15/2018 04:18:00 AM</td>
      <td>Harlem Park</td>
      <td>Western</td>
      <td>9.0</td>
      <td>(39.29431651, -76.6424061)</td>
    </tr>
    <tr>
      <th>1242</th>
      <td>64824</td>
      <td>T223430T</td>
      <td>12</td>
      <td>11.0</td>
      <td>MD</td>
      <td>CADI</td>
      <td>2527 LOYOLA SOUTHWAY</td>
      <td>22</td>
      <td>Expired Tags</td>
      <td>32.0</td>
      <td>...</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>05/07/2013 10:41:00 AM</td>
      <td>Greenspring</td>
      <td>Northern</td>
      <td>6.0</td>
      <td>2527 LOYOLA\nSOUTHWAY Baltimore, MD</td>
    </tr>
    <tr>
      <th>1582</th>
      <td>4988912</td>
      <td>3CL1965</td>
      <td>08</td>
      <td>18.0</td>
      <td>MD</td>
      <td>CHEV</td>
      <td>1200 BOLTON ST</td>
      <td>17</td>
      <td>Less Than 15 feet from Fire Hydrant</td>
      <td>77.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>03/23/2018 04:02:00 AM</td>
      <td>Bolton Hill</td>
      <td>Central</td>
      <td>11.0</td>
      <td>1200 BOLTON ST\nBaltimore, MD\n(39.304625, -76...</td>
    </tr>
    <tr>
      <th>1585</th>
      <td>5037933</td>
      <td>4DD9398</td>
      <td>01</td>
      <td>20.0</td>
      <td>MD</td>
      <td>GMC</td>
      <td>400 S MACON ST</td>
      <td>12</td>
      <td>No Stopping/Standing Not Tow-Away Zone</td>
      <td>32.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/06/2018 04:02:00 AM</td>
      <td>Greektown</td>
      <td>Southeastern</td>
      <td>1.0</td>
      <td>400 S MACON ST\nBaltimore, MD\n(39.287927, -76...</td>
    </tr>
    <tr>
      <th>1595</th>
      <td>21971684</td>
      <td>54086M9</td>
      <td>03</td>
      <td>14.0</td>
      <td>MD</td>
      <td>TOYOT</td>
      <td>700 ALICEANNA ST</td>
      <td>12</td>
      <td>No Stopping/Standing Not Tow-Away Zone</td>
      <td>32.0</td>
      <td>...</td>
      <td>357.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>300.0</td>
      <td>12/04/2013</td>
      <td>07/09/2015 04:02:00 AM</td>
      <td>Inner Harbor</td>
      <td>Southeastern</td>
      <td>1.0</td>
      <td>700 ALICEANNA ST\nBaltimore, MD\n(39.283111, -...</td>
    </tr>
    <tr>
      <th>1685</th>
      <td>20225108</td>
      <td>504M906</td>
      <td>03</td>
      <td>13.0</td>
      <td>MD</td>
      <td>JEEP</td>
      <td>1200 GITTINGS AVE</td>
      <td>22</td>
      <td>Expired Tags</td>
      <td>32.0</td>
      <td>...</td>
      <td>357.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>300.0</td>
      <td>04/24/2013</td>
      <td>11/12/2014 04:02:00 AM</td>
      <td>Idlewood</td>
      <td>Notheastern</td>
      <td>4.0</td>
      <td>1200 GITTINGS AVE\nBaltimore, MD\n(39.370213, ...</td>
    </tr>
    <tr>
      <th>2742</th>
      <td>63156484</td>
      <td>62401CG</td>
      <td>07</td>
      <td>18.0</td>
      <td>MD</td>
      <td>BMW</td>
      <td>3400 ELMORA AVE</td>
      <td>19</td>
      <td>Exceeding 48 Hours</td>
      <td>32.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>05/01/2018 04:02:00 AM</td>
      <td>Four By Four</td>
      <td>Notheastern</td>
      <td>13.0</td>
      <td>3400 ELMORA AVE\nBaltimore, MD\n(39.315891, -7...</td>
    </tr>
    <tr>
      <th>3392</th>
      <td>210831</td>
      <td>9AK3309</td>
      <td>10</td>
      <td>13.0</td>
      <td>MD</td>
      <td>DODG</td>
      <td>301 LIGHT ST</td>
      <td>5</td>
      <td>Obstruct/Impeding Movement of Pedestrian</td>
      <td>77.0</td>
      <td>...</td>
      <td>852.0</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>775.0</td>
      <td>09/20/2012</td>
      <td>08/09/2016 04:02:00 AM</td>
      <td>Inner Harbor</td>
      <td>Central</td>
      <td>11.0</td>
      <td>301 LIGHT ST\nBaltimore, MD\n(39.285066, -76.6...</td>
    </tr>
    <tr>
      <th>3550</th>
      <td>229385</td>
      <td>3RV727</td>
      <td>11</td>
      <td>13.0</td>
      <td>MD</td>
      <td>VOLV</td>
      <td>1200 BOLTON ST</td>
      <td>25</td>
      <td>Less 30 from Intersection</td>
      <td>32.0</td>
      <td>...</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>01/31/2018 08:34:00 PM</td>
      <td>Bolton Hill</td>
      <td>Central</td>
      <td>11.0</td>
      <td>1200 BOLTON ST\nBaltimore, MD\n(39.304625, -76...</td>
    </tr>
    <tr>
      <th>3640</th>
      <td>239038</td>
      <td>7BX5561</td>
      <td>04</td>
      <td>16.0</td>
      <td>MD</td>
      <td>HOND</td>
      <td>2010 BROENING HWY</td>
      <td>26</td>
      <td>No Stop/Park Handicap</td>
      <td>502.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>11/04/2015</td>
      <td>03/24/2016 04:02:00 AM</td>
      <td>Canton Industrial Area</td>
      <td>Southeastern</td>
      <td>1.0</td>
      <td>2010 BROENING HWY\nBaltimore, MD\n(39.267502, ...</td>
    </tr>
    <tr>
      <th>3641</th>
      <td>238022</td>
      <td>5BA6882</td>
      <td>04</td>
      <td>13.0</td>
      <td>MD</td>
      <td>NISS</td>
      <td>1700 MONTPELIER ST</td>
      <td>3</td>
      <td>Obstruct/Impeding Flow of Traffic</td>
      <td>102.0</td>
      <td>...</td>
      <td>1127.0</td>
      <td>NaN</td>
      <td>102.0</td>
      <td>672.0</td>
      <td>04/24/2013</td>
      <td>10/12/2016 04:02:00 AM</td>
      <td>Coldstream Homestead Montebello</td>
      <td>Notheastern</td>
      <td>14.0</td>
      <td>1700 MONTPELIER ST\nBaltimore, MD\n(39.319815,...</td>
    </tr>
    <tr>
      <th>3663</th>
      <td>239145</td>
      <td>39855CH</td>
      <td>04</td>
      <td>18.0</td>
      <td>MD</td>
      <td>LEXUS</td>
      <td>3716 BEEHLER AVE</td>
      <td>5</td>
      <td>Obstruct/Impeding Movement of Pedestrian</td>
      <td>77.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/11/2018 04:02:00 AM</td>
      <td>Central Park Heights</td>
      <td>Northwestern</td>
      <td>6.0</td>
      <td>3716 BEEHLER AVE\nBaltimore, MD\n(39.342319, -...</td>
    </tr>
    <tr>
      <th>4439</th>
      <td>328633</td>
      <td>AD46634</td>
      <td>00</td>
      <td>0.0</td>
      <td>AR</td>
      <td>FORD</td>
      <td>1800 BOLTON ST</td>
      <td>42</td>
      <td>Commercial Vehicle Obstruct/Imped Traffic Flow</td>
      <td>252.0</td>
      <td>...</td>
      <td>150.0</td>
      <td>NaN</td>
      <td>150.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>12/11/2012 04:04:00 AM</td>
      <td>Bolton Hill</td>
      <td>Central</td>
      <td>11.0</td>
      <td>1800 BOLTON ST\nBaltimore, MD\n(39.309367, -76...</td>
    </tr>
    <tr>
      <th>4458</th>
      <td>329250</td>
      <td>8AZ907</td>
      <td>12</td>
      <td>12.0</td>
      <td>MD</td>
      <td>CHEV</td>
      <td>1100 BOLTON ST</td>
      <td>5</td>
      <td>Obstruct/Impeding Movement of Pedestrian</td>
      <td>77.0</td>
      <td>...</td>
      <td>77.0</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>01/31/2018 08:34:00 PM</td>
      <td>Madison Park</td>
      <td>Central</td>
      <td>11.0</td>
      <td>1100 BOLTON ST\nBaltimore, MD\n(39.30354, -76....</td>
    </tr>
    <tr>
      <th>4597</th>
      <td>349761</td>
      <td>6AT0084</td>
      <td>07</td>
      <td>13.0</td>
      <td>MD</td>
      <td>TOYT</td>
      <td>600 N PULASKI ST</td>
      <td>19</td>
      <td>Exceeding 48 Hours</td>
      <td>32.0</td>
      <td>...</td>
      <td>332.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>300.0</td>
      <td>02/05/2013</td>
      <td>09/09/2014 04:02:00 AM</td>
      <td>Midtown-Edmondson</td>
      <td>Western</td>
      <td>9.0</td>
      <td>600 N PULASKI ST\nBaltimore, MD\n(39.295454, -...</td>
    </tr>
    <tr>
      <th>4664</th>
      <td>356055</td>
      <td>2447572T</td>
      <td>02</td>
      <td>14.0</td>
      <td>PA</td>
      <td>HOND</td>
      <td>1629 W NORTH AVE</td>
      <td>12</td>
      <td>No Stopping/Standing Not Tow-Away Zone</td>
      <td>32.0</td>
      <td>...</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>02/21/2014 04:02:00 AM</td>
      <td>Penn North</td>
      <td>Western</td>
      <td>7.0</td>
      <td>1629 W NORTH AVE\nBaltimore, MD\n(39.310046, -...</td>
    </tr>
    <tr>
      <th>4734</th>
      <td>362293</td>
      <td>1AK4764</td>
      <td>02</td>
      <td>14.0</td>
      <td>MD</td>
      <td>CHEV</td>
      <td>1500 APPLETON ST</td>
      <td>3</td>
      <td>Obstruct/Impeding Flow of Traffic</td>
      <td>102.0</td>
      <td>...</td>
      <td>1127.0</td>
      <td>NaN</td>
      <td>102.0</td>
      <td>761.0</td>
      <td>12/19/2012</td>
      <td>10/12/2016 04:02:00 AM</td>
      <td>Easterwood</td>
      <td>Western</td>
      <td>7.0</td>
      <td>1500 APPLETON ST\nBaltimore, MD\n(39.30533, -7...</td>
    </tr>
    <tr>
      <th>4735</th>
      <td>362566</td>
      <td>4AM9647</td>
      <td>01</td>
      <td>14.0</td>
      <td>MD</td>
      <td>LEXUS</td>
      <td>1501 APPLETON ST</td>
      <td>17</td>
      <td>Less Than 15 feet from Fire Hydrant</td>
      <td>77.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>688.0</td>
      <td>03/05/2013</td>
      <td>10/12/2016 04:02:00 AM</td>
      <td>Easterwood</td>
      <td>Western</td>
      <td>7.0</td>
      <td>1501 APPLETON ST\nBaltimore, MD\n(39.305313, -...</td>
    </tr>
    <tr>
      <th>4758</th>
      <td>364455</td>
      <td>XXN1568</td>
      <td>10</td>
      <td>11.0</td>
      <td>NC</td>
      <td>FORD</td>
      <td>1561 WADSWORTH WAY</td>
      <td>22</td>
      <td>Expired Tags</td>
      <td>32.0</td>
      <td>...</td>
      <td>332.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>300.0</td>
      <td>12/31/2012</td>
      <td>07/09/2014 04:02:00 AM</td>
      <td>Loch Raven</td>
      <td>Notheastern</td>
      <td>4.0</td>
      <td>1561 WADSWORTH WAY\nBaltimore, MD\n(39.362992,...</td>
    </tr>
    <tr>
      <th>4802</th>
      <td>365874</td>
      <td>D83038</td>
      <td>06</td>
      <td>12.0</td>
      <td>MD</td>
      <td>NaN</td>
      <td>300 E 30TH ST</td>
      <td>11</td>
      <td>Residential Parking Permit Only</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>500.0</td>
      <td>09/18/2012</td>
      <td>05/09/2015 04:01:00 AM</td>
      <td>Abell</td>
      <td>Northern</td>
      <td>14.0</td>
      <td>300 E 30TH ST\nBaltimore, MD\n(39.324624, -76....</td>
    </tr>
    <tr>
      <th>5300</th>
      <td>385336</td>
      <td>3FZD57</td>
      <td>05</td>
      <td>12.0</td>
      <td>MD</td>
      <td>NISS</td>
      <td>1800 N CAROLINE ST</td>
      <td>22</td>
      <td>Expired Tags</td>
      <td>32.0</td>
      <td>...</td>
      <td>332.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>300.0</td>
      <td>09/26/2012</td>
      <td>04/09/2014 04:01:00 AM</td>
      <td>Oliver</td>
      <td>Eastern</td>
      <td>12.0</td>
      <td>1800 N CAROLINE ST\nBaltimore, MD\n(39.310629,...</td>
    </tr>
    <tr>
      <th>5414</th>
      <td>5461661</td>
      <td>9CY4148</td>
      <td>07</td>
      <td>19.0</td>
      <td>MD</td>
      <td>HYUN</td>
      <td>400 E BALTIMORE ST</td>
      <td>46</td>
      <td>No Parking/Standing In Bus Stop/Bus Lane</td>
      <td>252.0</td>
      <td>...</td>
      <td>316.0</td>
      <td>NaN</td>
      <td>252.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>03/12/2019 04:03:00 AM</td>
      <td>Downtown</td>
      <td>Central</td>
      <td>11.0</td>
      <td>(39.28997272, -76.61002178)</td>
    </tr>
    <tr>
      <th>5432</th>
      <td>389304</td>
      <td>2AT1088</td>
      <td>08</td>
      <td>13.0</td>
      <td>MD</td>
      <td>HOND</td>
      <td>4300 NICHOLAS AVE</td>
      <td>22</td>
      <td>Expired Tags</td>
      <td>32.0</td>
      <td>...</td>
      <td>357.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>300.0</td>
      <td>10/01/2012</td>
      <td>04/09/2014 04:01:00 AM</td>
      <td>Belair-Edison</td>
      <td>Notheastern</td>
      <td>2.0</td>
      <td>4300 NICHOLAS AVE\nBaltimore, MD\n(39.327894, ...</td>
    </tr>
    <tr>
      <th>5436</th>
      <td>389064</td>
      <td>2MD1117</td>
      <td>05</td>
      <td>14.0</td>
      <td>MD</td>
      <td>VOLV</td>
      <td>1509 BANK ST</td>
      <td>22</td>
      <td>Expired Tags</td>
      <td>32.0</td>
      <td>...</td>
      <td>332.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>300.0</td>
      <td>10/03/2012</td>
      <td>05/09/2014 04:03:00 AM</td>
      <td>Fells Point</td>
      <td>Southeastern</td>
      <td>1.0</td>
      <td>1509 BANK ST\nBaltimore, MD\n(39.286473, -76.5...</td>
    </tr>
    <tr>
      <th>5467</th>
      <td>5461703</td>
      <td>1CT4531</td>
      <td>01</td>
      <td>20.0</td>
      <td>MD</td>
      <td>HOND</td>
      <td>200 N EUTAW ST</td>
      <td>12</td>
      <td>No Stopping/Standing Not Tow-Away Zone</td>
      <td>32.0</td>
      <td>...</td>
      <td>96.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>03/12/2019 04:03:00 AM</td>
      <td>Downtown</td>
      <td>Central</td>
      <td>11.0</td>
      <td>(39.29203643, -76.62180732)</td>
    </tr>
    <tr>
      <th>5498</th>
      <td>392951</td>
      <td>JLR240</td>
      <td>05</td>
      <td>15.0</td>
      <td>MD</td>
      <td>TOYT</td>
      <td>400 E 33RD ST</td>
      <td>12</td>
      <td>No Stopping/Standing Not Tow-Away Zone</td>
      <td>32.0</td>
      <td>...</td>
      <td>32.0</td>
      <td>NaN</td>
      <td>32.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>10/05/2013 04:04:00 AM</td>
      <td>Oakenshawe</td>
      <td>Northern</td>
      <td>14.0</td>
      <td>400 E 33RD ST\nBaltimore, MD\n(39.328372, -76....</td>
    </tr>
    <tr>
      <th>5501</th>
      <td>393454</td>
      <td>97M678</td>
      <td>08</td>
      <td>15.0</td>
      <td>MD</td>
      <td>FORD</td>
      <td>1600 CHILTON ST</td>
      <td>10</td>
      <td>Commercial Veh/Residence under 20,000 lbs</td>
      <td>252.0</td>
      <td>...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>02/04/2018 04:02:00 AM</td>
      <td>Coldstream Homestead Montebello</td>
      <td>Notheastern</td>
      <td>14.0</td>
      <td>1600 CHILTON ST\nBaltimore, MD\n(39.327509, -7...</td>
    </tr>
    <tr>
      <th>5527</th>
      <td>394155</td>
      <td>1BF5281</td>
      <td>09</td>
      <td>15.0</td>
      <td>MD</td>
      <td>NISS</td>
      <td>100 N LUZERNE AVE</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>525.0</td>
      <td>10/23/2013</td>
      <td>06/09/2016 04:02:00 AM</td>
      <td>Patterson Park Neighborhood</td>
      <td>Southeastern</td>
      <td>1.0</td>
      <td>100 N LUZERNE AVE\nBaltimore, MD\n(39.293291, ...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3385186</th>
      <td>97808415</td>
      <td>4CK4945</td>
      <td>07</td>
      <td>16.0</td>
      <td>MD</td>
      <td>ACURA</td>
      <td>2000 LINDEN AVE</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/14/2016</td>
      <td>10/12/2016 04:02:00 AM</td>
      <td>Reservoir Hill</td>
      <td>Central</td>
      <td>7.0</td>
      <td>2000 LINDEN AVE\nBaltimore, MD\n(39.311176, -7...</td>
    </tr>
    <tr>
      <th>3385187</th>
      <td>97748272</td>
      <td>5CM0925</td>
      <td>09</td>
      <td>16.0</td>
      <td>MD</td>
      <td>LINCO</td>
      <td>2400 CALLOW AVE</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/14/2016</td>
      <td>10/12/2016 04:02:00 AM</td>
      <td>Reservoir Hill</td>
      <td>Central</td>
      <td>7.0</td>
      <td>2400 CALLOW AVE\nBaltimore, MD\n(39.314549, -7...</td>
    </tr>
    <tr>
      <th>3385188</th>
      <td>97760665</td>
      <td>5CG6841</td>
      <td>03</td>
      <td>17.0</td>
      <td>MD</td>
      <td>FORD</td>
      <td>1800 BAKER ST</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/14/2016</td>
      <td>10/12/2016 04:02:00 AM</td>
      <td>Sandtown-Winchester</td>
      <td>Western</td>
      <td>7.0</td>
      <td>1800 BAKER ST\nBaltimore, MD\n(39.30662, -76.6...</td>
    </tr>
    <tr>
      <th>3385190</th>
      <td>97748330</td>
      <td>6CD5903</td>
      <td>05</td>
      <td>17.0</td>
      <td>MD</td>
      <td>CHEVR</td>
      <td>2400 FRANCIS ST</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/14/2016</td>
      <td>10/12/2016 04:02:00 AM</td>
      <td>Penn North</td>
      <td>Western</td>
      <td>7.0</td>
      <td>2400 FRANCIS ST\nBaltimore, MD\n(39.311265, -7...</td>
    </tr>
    <tr>
      <th>3385191</th>
      <td>97817366</td>
      <td>8CG2815</td>
      <td>04</td>
      <td>17.0</td>
      <td>MD</td>
      <td>PONTI</td>
      <td>800 APPLETON ST</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/21/2016</td>
      <td>10/18/2016 04:01:00 AM</td>
      <td>Midtown-Edmondson</td>
      <td>Western</td>
      <td>9.0</td>
      <td>800 APPLETON ST\nBaltimore, MD\n(39.297892, -7...</td>
    </tr>
    <tr>
      <th>3385193</th>
      <td>97759733</td>
      <td>ACH689</td>
      <td>05</td>
      <td>17.0</td>
      <td>MD</td>
      <td>TOYOT</td>
      <td>3200 BARCLAY ST</td>
      <td>11</td>
      <td>Residential Parking Permit Only</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/21/2016</td>
      <td>10/18/2016 04:01:00 AM</td>
      <td>Abell</td>
      <td>Northern</td>
      <td>14.0</td>
      <td>3200 BARCLAY ST\nBaltimore, MD\n(39.327233, -7...</td>
    </tr>
    <tr>
      <th>3385195</th>
      <td>97834981</td>
      <td>7CH2118</td>
      <td>05</td>
      <td>18.0</td>
      <td>MD</td>
      <td>TOYOT</td>
      <td>3000 GREENMOUNT AVE</td>
      <td>8</td>
      <td>No Stopping/Standing Tow Away Zone</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/21/2016</td>
      <td>10/18/2016 04:01:00 AM</td>
      <td>Abell</td>
      <td>Northern</td>
      <td>14.0</td>
      <td>3000 GREENMOUNT AVE\nBaltimore, MD\n(39.324958...</td>
    </tr>
    <tr>
      <th>3385200</th>
      <td>97825526</td>
      <td>5CJ3792</td>
      <td>07</td>
      <td>17.0</td>
      <td>MD</td>
      <td>VOLKS</td>
      <td>700 BARTLETT AVE</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/21/2016</td>
      <td>10/18/2016 04:01:00 AM</td>
      <td>East Baltimore Midway</td>
      <td>Eastern</td>
      <td>12.0</td>
      <td>700 BARTLETT AVE\nBaltimore, MD\n(39.316109, -...</td>
    </tr>
    <tr>
      <th>3385205</th>
      <td>97717970</td>
      <td>2BL5561</td>
      <td>12</td>
      <td>16.0</td>
      <td>MD</td>
      <td>ACURA</td>
      <td>2600 AISQUITH ST</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/14/2016</td>
      <td>10/12/2016 04:02:00 AM</td>
      <td>Coldstream Homestead Montebello</td>
      <td>Notheastern</td>
      <td>14.0</td>
      <td>2600 AISQUITH ST\nBaltimore, MD\n(39.31903, -7...</td>
    </tr>
    <tr>
      <th>3385207</th>
      <td>97981097</td>
      <td>9BN7663</td>
      <td>07</td>
      <td>17.0</td>
      <td>MD</td>
      <td>ACURA</td>
      <td>3100 GREENMOUNT AVE</td>
      <td>8</td>
      <td>No Stopping/Standing Tow Away Zone</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/10/2016 04:02:00 AM</td>
      <td>Abell</td>
      <td>Northern</td>
      <td>14.0</td>
      <td>3100 GREENMOUNT AVE\nBaltimore, MD\n(39.326252...</td>
    </tr>
    <tr>
      <th>3385211</th>
      <td>97930144</td>
      <td>0809Z0</td>
      <td>03</td>
      <td>18.0</td>
      <td>MD</td>
      <td>CHEVR</td>
      <td>2900 MOSHER ST</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/21/2016</td>
      <td>10/18/2016 04:01:00 AM</td>
      <td>Franklintown Road</td>
      <td>Southwestern</td>
      <td>9.0</td>
      <td>2900 MOSHER ST\nBaltimore, MD\n(39.299166, -76...</td>
    </tr>
    <tr>
      <th>3385217</th>
      <td>97916713</td>
      <td>8BG7823</td>
      <td>04</td>
      <td>16.0</td>
      <td>MD</td>
      <td>CADIL</td>
      <td>2300 CALLOW AVE</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/14/2016</td>
      <td>10/12/2016 04:02:00 AM</td>
      <td>Reservoir Hill</td>
      <td>Central</td>
      <td>7.0</td>
      <td>2300 CALLOW AVE\nBaltimore, MD\n(39.313746, -7...</td>
    </tr>
    <tr>
      <th>3385221</th>
      <td>97991450</td>
      <td>5CD2575</td>
      <td>10</td>
      <td>16.0</td>
      <td>MD</td>
      <td>BUICK</td>
      <td>2500 LAURETTA AVE</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/13/2016 04:02:00 AM</td>
      <td>Rosemont Homeowners/Tenants</td>
      <td>Western</td>
      <td>9.0</td>
      <td>2500 LAURETTA AVE\nBaltimore, MD\n(39.294041, ...</td>
    </tr>
    <tr>
      <th>3385222</th>
      <td>97928544</td>
      <td>Z75017</td>
      <td>11</td>
      <td>17.0</td>
      <td>MD</td>
      <td>CHEVR</td>
      <td>4000 OAKFORD AVE</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/10/2016 04:02:00 AM</td>
      <td>West Arlington</td>
      <td>Northwestern</td>
      <td>6.0</td>
      <td>4000 OAKFORD AVE\nBaltimore, MD\n(39.335821, -...</td>
    </tr>
    <tr>
      <th>3385224</th>
      <td>97987730</td>
      <td>9CD8533</td>
      <td>11</td>
      <td>17.0</td>
      <td>MD</td>
      <td>NISSA</td>
      <td>3200 GREENMOUNT AVE</td>
      <td>8</td>
      <td>No Stopping/Standing Tow Away Zone</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/10/2016 04:02:00 AM</td>
      <td>Abell</td>
      <td>Northern</td>
      <td>14.0</td>
      <td>3200 GREENMOUNT AVE\nBaltimore, MD\n(39.327394...</td>
    </tr>
    <tr>
      <th>3385226</th>
      <td>97994751</td>
      <td>7BK0252</td>
      <td>03</td>
      <td>18.0</td>
      <td>MD</td>
      <td>CHEVR</td>
      <td>5000 WABASH AVE</td>
      <td>8</td>
      <td>No Stopping/Standing Tow Away Zone</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/13/2016 04:02:00 AM</td>
      <td>Dolfield</td>
      <td>Northwestern</td>
      <td>6.0</td>
      <td>5000 WABASH AVE\nBaltimore, MD\n(39.341626, -7...</td>
    </tr>
    <tr>
      <th>3385230</th>
      <td>97931720</td>
      <td>5BW2419</td>
      <td>04</td>
      <td>17.0</td>
      <td>MD</td>
      <td>HONDA</td>
      <td>4000 EDMONDSON AVE</td>
      <td>8</td>
      <td>No Stopping/Standing Tow Away Zone</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/14/2016 04:02:00 AM</td>
      <td>Edmondson Village</td>
      <td>Southwestern</td>
      <td>8.0</td>
      <td>4000 EDMONDSON AVE\nBaltimore, MD\n(39.29381, ...</td>
    </tr>
    <tr>
      <th>3385231</th>
      <td>98021448</td>
      <td>5CK1963</td>
      <td>07</td>
      <td>16.0</td>
      <td>MD</td>
      <td>FORD</td>
      <td>2700 THE ALAMEDA</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/16/2016 04:02:00 AM</td>
      <td>Coldstream Homestead Montebello</td>
      <td>Notheastern</td>
      <td>14.0</td>
      <td>2700 THE\nALAMEDA Baltimore, MD\n(35.030949, -...</td>
    </tr>
    <tr>
      <th>3385235</th>
      <td>97968110</td>
      <td>6BV7344</td>
      <td>01</td>
      <td>17.0</td>
      <td>MD</td>
      <td>TOYOT</td>
      <td>300 WARREN AVE</td>
      <td>11</td>
      <td>Residential Parking Permit Only</td>
      <td>52.0</td>
      <td>...</td>
      <td>525.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>16.0</td>
      <td>09/21/2016</td>
      <td>10/18/2016 04:01:00 AM</td>
      <td>Federal Hill</td>
      <td>Southern</td>
      <td>11.0</td>
      <td>300 WARREN AVE\nBaltimore, MD\n(39.279055, -76...</td>
    </tr>
    <tr>
      <th>3385237</th>
      <td>97997861</td>
      <td>16459CG</td>
      <td>04</td>
      <td>17.0</td>
      <td>MD</td>
      <td>BMW</td>
      <td>900 LIGHT ST</td>
      <td>8</td>
      <td>No Stopping/Standing Tow Away Zone</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>09/28/2016</td>
      <td>09/29/2016 04:02:00 AM</td>
      <td>Federal Hill</td>
      <td>Southern</td>
      <td>11.0</td>
      <td>900 LIGHT ST\nBaltimore, MD\n(39.278948, -76.6...</td>
    </tr>
    <tr>
      <th>3385238</th>
      <td>97902879</td>
      <td>7AA6866</td>
      <td>12</td>
      <td>16.0</td>
      <td>MD</td>
      <td>PONTI</td>
      <td>800 LIGHT ST</td>
      <td>8</td>
      <td>No Stopping/Standing Tow Away Zone</td>
      <td>52.0</td>
      <td>...</td>
      <td>502.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/24/2016 04:02:00 AM</td>
      <td>Federal Hill</td>
      <td>Southern</td>
      <td>11.0</td>
      <td>800 LIGHT ST\nBaltimore, MD\n(39.279788, -76.6...</td>
    </tr>
    <tr>
      <th>3385241</th>
      <td>97895024</td>
      <td>4CG6630</td>
      <td>05</td>
      <td>18.0</td>
      <td>MD</td>
      <td>HONDA</td>
      <td>2700 THE ALAMEDA</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>09/28/2016</td>
      <td>09/29/2016 04:02:00 AM</td>
      <td>Coldstream Homestead Montebello</td>
      <td>Notheastern</td>
      <td>14.0</td>
      <td>2700 THE\nALAMEDA Baltimore, MD\n(35.030949, -...</td>
    </tr>
    <tr>
      <th>3385243</th>
      <td>97921168</td>
      <td>6BF9322</td>
      <td>12</td>
      <td>17.0</td>
      <td>MD</td>
      <td>DODGE</td>
      <td>2500 MCCULLOH ST</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>09/28/2016</td>
      <td>09/29/2016 04:02:00 AM</td>
      <td>Penn North</td>
      <td>Western</td>
      <td>7.0</td>
      <td>2500 MCCULLOH ST\nBaltimore, MD\n(39.313019, -...</td>
    </tr>
    <tr>
      <th>3385244</th>
      <td>98005151</td>
      <td>5BN7602</td>
      <td>06</td>
      <td>17.0</td>
      <td>MD</td>
      <td>JEEP</td>
      <td>3718 CLAREMONT ST</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/24/2016 04:02:00 AM</td>
      <td>Highlandtown</td>
      <td>Southeastern</td>
      <td>2.0</td>
      <td>3718 CLAREMONT ST\nBaltimore, MD\n(39.289487, ...</td>
    </tr>
    <tr>
      <th>3385247</th>
      <td>98163612</td>
      <td>9CM2854</td>
      <td>10</td>
      <td>16.0</td>
      <td>MD</td>
      <td>HYUND</td>
      <td>1700 HOMESTEAD ST</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>10/13/2016 04:02:00 AM</td>
      <td>Coldstream Homestead Montebello</td>
      <td>Notheastern</td>
      <td>14.0</td>
      <td>1700 HOMESTEAD ST\nBaltimore, MD\n(39.320347, ...</td>
    </tr>
    <tr>
      <th>3385252</th>
      <td>97906870</td>
      <td>948TBG</td>
      <td>10</td>
      <td>16.0</td>
      <td>TN</td>
      <td>JAGUA</td>
      <td>4700 LOCH RAVEN BLVD</td>
      <td>16</td>
      <td>No Parking/Standing In Transit Stop</td>
      <td>77.0</td>
      <td>...</td>
      <td>557.0</td>
      <td>NaN</td>
      <td>77.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/10/2016 04:02:00 AM</td>
      <td>New Northwood</td>
      <td>Notheastern</td>
      <td>4.0</td>
      <td>4700 LOCH RAVEN BLVD\nBaltimore, MD\n(39.34785...</td>
    </tr>
    <tr>
      <th>3385255</th>
      <td>98317325</td>
      <td>8CJ0436</td>
      <td>07</td>
      <td>17.0</td>
      <td>MD</td>
      <td>NISSA</td>
      <td>1200 OAKHURST PL</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>552.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>10/18/2016 04:01:00 AM</td>
      <td>Winchester</td>
      <td>Southwestern</td>
      <td>9.0</td>
      <td>1200 OAKHURST PL\nBaltimore, MD\n(39.301794, -...</td>
    </tr>
    <tr>
      <th>3385262</th>
      <td>98321061</td>
      <td>9CL2241</td>
      <td>09</td>
      <td>16.0</td>
      <td>MD</td>
      <td>FORD</td>
      <td>2800 ROSALIND AVE</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>10/14/2016 04:02:00 AM</td>
      <td>Cylburn</td>
      <td>Northern</td>
      <td>6.0</td>
      <td>2800 ROSALIND AVE\nBaltimore, MD\n(39.34593, -...</td>
    </tr>
    <tr>
      <th>3385266</th>
      <td>98306641</td>
      <td>5CF3889</td>
      <td>02</td>
      <td>18.0</td>
      <td>MD</td>
      <td>HYUND</td>
      <td>1700 RUXTON AVE</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>602.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>10/13/2016 04:02:00 AM</td>
      <td>Coppin Heights/Ash-Co-East</td>
      <td>Western</td>
      <td>7.0</td>
      <td>1700 RUXTON AVE\nBaltimore, MD\n(39.307742, -7...</td>
    </tr>
    <tr>
      <th>3385267</th>
      <td>98278832</td>
      <td>8CL2458</td>
      <td>09</td>
      <td>17.0</td>
      <td>MD</td>
      <td>PONTI</td>
      <td>3000 MCELDERRY ST</td>
      <td>27</td>
      <td>No Stop/Park Street Cleaning</td>
      <td>52.0</td>
      <td>...</td>
      <td>577.0</td>
      <td>NaN</td>
      <td>52.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>10/13/2016 04:02:00 AM</td>
      <td>Ellwood Park/Monument</td>
      <td>Southeastern</td>
      <td>13.0</td>
      <td>3000 MCELDERRY ST\nBaltimore, MD\n(39.298026, ...</td>
    </tr>
  </tbody>
</table>
<p>345242 rows × 21 columns</p>
</div>




```python
pol_dist = cite2['PoliceDistrict'].notna().sum()
pol_dist
```




    345242




```python
poldis_df = pol_dis.apply(lambda x: x.astype(str).str.lower())
poldis_df.dtypes
poldis_df['ViolFine'] = pd.to_numeric(poldis_df['ViolFine'])
```


```python
poldis_vf = poldis_df.groupby('PoliceDistrict')['ViolFine'].mean()
pdvf = poldis_vf.to_frame()
pdvf.reset_index(0, inplace=True)
pdvf
#pdvf.columns = pdvf.columns.str.strip().str.replace(' ','')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PoliceDistrict</th>
      <th>ViolFine</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>central</td>
      <td>44.816352</td>
    </tr>
    <tr>
      <th>1</th>
      <td>eastern</td>
      <td>50.800873</td>
    </tr>
    <tr>
      <th>2</th>
      <td>northeastern</td>
      <td>52.120643</td>
    </tr>
    <tr>
      <th>3</th>
      <td>northern</td>
      <td>48.144727</td>
    </tr>
    <tr>
      <th>4</th>
      <td>northwestern</td>
      <td>59.690660</td>
    </tr>
    <tr>
      <th>5</th>
      <td>notheastern</td>
      <td>62.054571</td>
    </tr>
    <tr>
      <th>6</th>
      <td>southeastern</td>
      <td>48.750365</td>
    </tr>
    <tr>
      <th>7</th>
      <td>southern</td>
      <td>54.391261</td>
    </tr>
    <tr>
      <th>8</th>
      <td>southwestern</td>
      <td>58.283804</td>
    </tr>
    <tr>
      <th>9</th>
      <td>western</td>
      <td>53.526153</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python
pdvf.groupby(['PoliceDistrict'].agg['ViolFine'].mean())
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-201-2862cb531192> in <module>
    ----> 1 pdvf.groupby(['PoliceDistrict'].agg['ViolFine'].mean())
    

    AttributeError: 'list' object has no attribute 'agg'



```python
if pdvf['PoliceDistrict']=="notheastern":
    
```


```python
pol_dis_array = pol_dis.PoliceDistrict.value_counts()
pol_dis_array
```




    Southeastern    63982
    Central         58388
    Southern        54643
    Northern        42492
    Notheastern     24592
    Eastern         20743
    Western         17886
    Southwestern    15749
    Northwestern    12859
    SOUTHEASTERN     8600
    SOUTHERN         7083
    CENTRAL          6437
    NORTHERN         5419
    NORTHEASTERN     1865
    EASTERN          1489
    SOUTHWESTERN     1150
    WESTERN          1137
    NORTHWESTERN      728
    Name: PoliceDistrict, dtype: int64




```python
type(pol_dis_array)
```




    pandas.core.series.Series




```python
pol_dis_array.count()
```




    18




```python
dist_df = pol_dis_array.to_frame()
dist_df.index
```




    Index(['Southeastern', 'Central', 'Southern', 'Northern', 'Notheastern',
           'Eastern', 'Western', 'Southwestern', 'Northwestern', 'SOUTHEASTERN',
           'SOUTHERN', 'CENTRAL', 'NORTHERN', 'NORTHEASTERN', 'EASTERN',
           'SOUTHWESTERN', 'WESTERN', 'NORTHWESTERN'],
          dtype='object')




```python
dist_df.reset_index(0,inplace=True)
```


```python
#dist_df.values
#[x * y - z for x, y, z in zip(df2['apples'], df2['oranges'], df2['bananas'])]
df2 = dist_df.apply(lambda x: x.astype(str).str.lower())
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>PoliceDistrict</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>southeastern</td>
      <td>63982</td>
    </tr>
    <tr>
      <th>1</th>
      <td>central</td>
      <td>58388</td>
    </tr>
    <tr>
      <th>2</th>
      <td>southern</td>
      <td>54643</td>
    </tr>
    <tr>
      <th>3</th>
      <td>northern</td>
      <td>42492</td>
    </tr>
    <tr>
      <th>4</th>
      <td>notheastern</td>
      <td>24592</td>
    </tr>
    <tr>
      <th>5</th>
      <td>eastern</td>
      <td>20743</td>
    </tr>
    <tr>
      <th>6</th>
      <td>western</td>
      <td>17886</td>
    </tr>
    <tr>
      <th>7</th>
      <td>southwestern</td>
      <td>15749</td>
    </tr>
    <tr>
      <th>8</th>
      <td>northwestern</td>
      <td>12859</td>
    </tr>
    <tr>
      <th>9</th>
      <td>southeastern</td>
      <td>8600</td>
    </tr>
    <tr>
      <th>10</th>
      <td>southern</td>
      <td>7083</td>
    </tr>
    <tr>
      <th>11</th>
      <td>central</td>
      <td>6437</td>
    </tr>
    <tr>
      <th>12</th>
      <td>northern</td>
      <td>5419</td>
    </tr>
    <tr>
      <th>13</th>
      <td>northeastern</td>
      <td>1865</td>
    </tr>
    <tr>
      <th>14</th>
      <td>eastern</td>
      <td>1489</td>
    </tr>
    <tr>
      <th>15</th>
      <td>southwestern</td>
      <td>1150</td>
    </tr>
    <tr>
      <th>16</th>
      <td>western</td>
      <td>1137</td>
    </tr>
    <tr>
      <th>17</th>
      <td>northwestern</td>
      <td>728</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.dtypes
df2['PoliceDistrict'] = pd.to_numeric(df2['PoliceDistrict'])
```


```python
#df2.groupby(['index'])['PoliceDistrict'].sum().reset_index()
df2.groupby('index').sum()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PoliceDistrict</th>
    </tr>
    <tr>
      <th>index</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>central</th>
      <td>64825</td>
    </tr>
    <tr>
      <th>eastern</th>
      <td>22232</td>
    </tr>
    <tr>
      <th>northeastern</th>
      <td>1865</td>
    </tr>
    <tr>
      <th>northern</th>
      <td>47911</td>
    </tr>
    <tr>
      <th>northwestern</th>
      <td>13587</td>
    </tr>
    <tr>
      <th>notheastern</th>
      <td>24592</td>
    </tr>
    <tr>
      <th>southeastern</th>
      <td>72582</td>
    </tr>
    <tr>
      <th>southern</th>
      <td>61726</td>
    </tr>
    <tr>
      <th>southwestern</th>
      <td>16899</td>
    </tr>
    <tr>
      <th>western</th>
      <td>19023</td>
    </tr>
  </tbody>
</table>
</div>



## Find the ten vehicle makes that received the most citations during 2017. For those top ten, find all Japanese-made vehicles. What proportion of all citations were written for those vehicles? Note that the naming in Make is not consistent over the whole dataset, so you will need to clean the data before calculating your answer. Your answer should be expressed as a decimal number (i.e. 0.42, not 42).


```python
from datetime import datetime
cite2['year'] = pd.DatetimeIndex(cite2['ViolDate']).year
cite2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Citation</th>
      <th>Tag</th>
      <th>ExpMM</th>
      <th>ExpYY</th>
      <th>State</th>
      <th>Make</th>
      <th>Address</th>
      <th>ViolCode</th>
      <th>Description</th>
      <th>ViolFine</th>
      <th>...</th>
      <th>PenaltyDate</th>
      <th>OpenFine</th>
      <th>OpenPenalty</th>
      <th>NoticeDate</th>
      <th>ImportDate</th>
      <th>Neighborhood</th>
      <th>PoliceDistrict</th>
      <th>CouncilDistrict</th>
      <th>Location</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>82691651</td>
      <td>69943CF</td>
      <td>04</td>
      <td>19.0</td>
      <td>MD</td>
      <td>MAZD</td>
      <td>1300 BLK EAST NORTHERN PKWY WB</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/26/2018 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1300 BLK EAST NORTHERN PKWY\nWB Baltimore, MD\...</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>85937226</td>
      <td>T720887</td>
      <td>12</td>
      <td>18.0</td>
      <td>MD</td>
      <td>ACUR</td>
      <td>300 BLK NORTH BEND RD SB</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>01/03/2019 04:33:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>82691115</td>
      <td>5BA2678</td>
      <td>03</td>
      <td>19.0</td>
      <td>MD</td>
      <td>TOYT</td>
      <td>5000 BLK ROLAND AVE NB</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/26/2018 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5000 BLK ROLAND AVE\nNB Baltimore, MD\n(39.353...</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>82694689</td>
      <td>5BT8544</td>
      <td>01</td>
      <td>18.0</td>
      <td>MD</td>
      <td>FORD</td>
      <td>2400 BLK ERDMAN AVE NB</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/26/2018 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2400 BLK ERDMAN AVE\nNB Baltimore, MD\n(39.325...</td>
      <td>2018.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>82691214</td>
      <td>1BV0537</td>
      <td>11</td>
      <td>18.0</td>
      <td>MD</td>
      <td>SUBA</td>
      <td>1300 BLK WEST COLD SPRING LN W</td>
      <td>32</td>
      <td>Fixed Speed Camera</td>
      <td>40.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>04/26/2018 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1300 BLK WEST COLD SPRING LN W\nBaltimore, MD\...</td>
      <td>2018.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
cite2['year'].dtype
```




    dtype('float64')




```python
cite_year2017 = cite2[cite2.year == 2017.0]
cite_year2017.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Citation</th>
      <th>Tag</th>
      <th>ExpMM</th>
      <th>ExpYY</th>
      <th>State</th>
      <th>Make</th>
      <th>Address</th>
      <th>ViolCode</th>
      <th>Description</th>
      <th>ViolFine</th>
      <th>...</th>
      <th>PenaltyDate</th>
      <th>OpenFine</th>
      <th>OpenPenalty</th>
      <th>NoticeDate</th>
      <th>ImportDate</th>
      <th>Neighborhood</th>
      <th>PoliceDistrict</th>
      <th>CouncilDistrict</th>
      <th>Location</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>631</th>
      <td>50013862</td>
      <td>7AC9218</td>
      <td>01</td>
      <td>19.0</td>
      <td>MD</td>
      <td>TOYT</td>
      <td>E North AVE WB @ N Howard St</td>
      <td>30</td>
      <td>Red Light Violation</td>
      <td>75.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>09/20/2017 04:03:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>E N North AVE WB\nBaltimore, MD</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>676</th>
      <td>50097410</td>
      <td>2EYW11</td>
      <td>04</td>
      <td>19.0</td>
      <td>MD</td>
      <td>HOND</td>
      <td>Loch Raven Blvd NB @ E Belvede</td>
      <td>30</td>
      <td>Red Light Violation</td>
      <td>75.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>10/21/2017 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>E Loch Raven Blvd NB\nBaltimore, MD</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>698</th>
      <td>50129379</td>
      <td>LB0393</td>
      <td>00</td>
      <td>0.0</td>
      <td>MD</td>
      <td>MERZ</td>
      <td>Loch Raven Blvd SB @ E Belvede</td>
      <td>30</td>
      <td>Red Light Violation</td>
      <td>75.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>10/31/2017 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>E Loch Raven Blvd SB\nBaltimore, MD</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>703</th>
      <td>50131359</td>
      <td>5BP5889</td>
      <td>00</td>
      <td>0.0</td>
      <td>MD</td>
      <td>FORD</td>
      <td>Pulaski Hwy EB @ N North Point</td>
      <td>30</td>
      <td>Red Light Violation</td>
      <td>75.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>10/31/2017 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>N Pulaski Hwy EB\nBaltimore, MD</td>
      <td>2017.0</td>
    </tr>
    <tr>
      <th>726</th>
      <td>50151134</td>
      <td>3CY2133</td>
      <td>00</td>
      <td>0.0</td>
      <td>MD</td>
      <td>NISS</td>
      <td>Pulaski Hwy EB @ Moravia Park</td>
      <td>30</td>
      <td>Red Light Violation</td>
      <td>75.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>11/03/2017 04:02:00 AM</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Pulaski Hwy EB\nBaltimore, MD</td>
      <td>2017.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
cite_year2017.Make.mode()
```




    0    FORD
    dtype: object




```python
top2017 = cite_year2017.groupby(['year', 'Make']).year.value_counts().nlargest(10)
top2017df = top2017.to_frame()
top2017df
# top2017df.set_index(['Make'], inplace=True, append = True, drop = True)

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th></th>
      <th>year</th>
    </tr>
    <tr>
      <th>year</th>
      <th>Make</th>
      <th>year</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="10" valign="top">2017.0</th>
      <th>FORD</th>
      <th>2017.0</th>
      <td>56786</td>
    </tr>
    <tr>
      <th>HONDA</th>
      <th>2017.0</th>
      <td>43049</td>
    </tr>
    <tr>
      <th>TOYOT</th>
      <th>2017.0</th>
      <td>40844</td>
    </tr>
    <tr>
      <th>NISSA</th>
      <th>2017.0</th>
      <td>27991</td>
    </tr>
    <tr>
      <th>CHEVR</th>
      <th>2017.0</th>
      <td>27745</td>
    </tr>
    <tr>
      <th>TOYT</th>
      <th>2017.0</th>
      <td>27590</td>
    </tr>
    <tr>
      <th>HOND</th>
      <th>2017.0</th>
      <td>27368</td>
    </tr>
    <tr>
      <th>NISS</th>
      <th>2017.0</th>
      <td>22014</td>
    </tr>
    <tr>
      <th>CHEV</th>
      <th>2017.0</th>
      <td>21705</td>
    </tr>
    <tr>
      <th>JEEP</th>
      <th>2017.0</th>
      <td>16973</td>
    </tr>
  </tbody>
</table>
</div>




```python
totalcite17 = cite_year2017.year.value_counts().sum()
totalcite17
```




    553981




```python
japcars = 43049+40844+27991+27590+27368+22014
japcars
```




    188856




```python
japcars/totalcite17
```




    0.34090699861547596




```python
cite2yrs = cite2.groupby(['year']).sum()
cite2yrs.reset_index(level=0, inplace=True)
cite2yrs
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>Citation</th>
      <th>ExpYY</th>
      <th>ViolCode</th>
      <th>ViolFine</th>
      <th>Balance</th>
      <th>PenaltyDate</th>
      <th>OpenFine</th>
      <th>OpenPenalty</th>
      <th>CouncilDistrict</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1999.0</td>
      <td>40231789</td>
      <td>0.0</td>
      <td>30</td>
      <td>75.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000.0</td>
      <td>123437109</td>
      <td>5.0</td>
      <td>90</td>
      <td>225.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002.0</td>
      <td>2553370481</td>
      <td>267.0</td>
      <td>1740</td>
      <td>4350.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2003.0</td>
      <td>6787273770</td>
      <td>671.0</td>
      <td>4440</td>
      <td>11100.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2004.0</td>
      <td>5929909208</td>
      <td>1142.0</td>
      <td>3860</td>
      <td>7985.0</td>
      <td>8240.0</td>
      <td>0.0</td>
      <td>3673.0</td>
      <td>2155.0</td>
      <td>58.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2005.0</td>
      <td>40143341317</td>
      <td>7438.0</td>
      <td>23573</td>
      <td>44565.0</td>
      <td>50852.0</td>
      <td>0.0</td>
      <td>40655.0</td>
      <td>4870.0</td>
      <td>510.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2006.0</td>
      <td>325847089541</td>
      <td>39841.0</td>
      <td>128173</td>
      <td>204672.0</td>
      <td>255737.0</td>
      <td>0.0</td>
      <td>196211.0</td>
      <td>3570.0</td>
      <td>2094.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2007.0</td>
      <td>3274128266047</td>
      <td>381597.0</td>
      <td>1138640</td>
      <td>1915819.0</td>
      <td>2252863.0</td>
      <td>0.0</td>
      <td>1903316.0</td>
      <td>23343.0</td>
      <td>40565.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2008.0</td>
      <td>2730980171881</td>
      <td>356333.0</td>
      <td>884699</td>
      <td>1579975.0</td>
      <td>1817096.0</td>
      <td>0.0</td>
      <td>1561574.0</td>
      <td>12030.0</td>
      <td>57745.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2009.0</td>
      <td>2936647980524</td>
      <td>404338.0</td>
      <td>889395</td>
      <td>1653234.0</td>
      <td>1842377.0</td>
      <td>0.0</td>
      <td>1608374.0</td>
      <td>228185.0</td>
      <td>58937.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2010.0</td>
      <td>3728444379924</td>
      <td>481453.0</td>
      <td>967703</td>
      <td>1973124.0</td>
      <td>2131881.0</td>
      <td>0.0</td>
      <td>1927679.0</td>
      <td>159457.0</td>
      <td>82724.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2011.0</td>
      <td>10805799688122</td>
      <td>1482399.0</td>
      <td>3676969</td>
      <td>6358346.0</td>
      <td>18331275.0</td>
      <td>0.0</td>
      <td>6272580.0</td>
      <td>13322533.0</td>
      <td>92867.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2012.0</td>
      <td>6763628192955</td>
      <td>1939530.0</td>
      <td>4609708</td>
      <td>7843721.0</td>
      <td>18421078.0</td>
      <td>0.0</td>
      <td>7001911.0</td>
      <td>12521072.0</td>
      <td>106336.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2013.0</td>
      <td>1718882502872</td>
      <td>720176.0</td>
      <td>1186059</td>
      <td>2889470.0</td>
      <td>12884423.0</td>
      <td>0.0</td>
      <td>2220923.0</td>
      <td>11615391.0</td>
      <td>89305.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2014.0</td>
      <td>4256522079363</td>
      <td>1148855.0</td>
      <td>1643654</td>
      <td>4210955.0</td>
      <td>12887230.0</td>
      <td>0.0</td>
      <td>2308770.0</td>
      <td>11035398.0</td>
      <td>133480.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2015.0</td>
      <td>31470855699741</td>
      <td>5485300.0</td>
      <td>7132276</td>
      <td>16373563.0</td>
      <td>13275068.0</td>
      <td>0.0</td>
      <td>2830878.0</td>
      <td>8163712.0</td>
      <td>510376.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2016.0</td>
      <td>32644033406144</td>
      <td>5726222.0</td>
      <td>7099195</td>
      <td>16751740.0</td>
      <td>13700476.0</td>
      <td>0.0</td>
      <td>8148758.0</td>
      <td>2581124.0</td>
      <td>510976.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2017.0</td>
      <td>39607232779820</td>
      <td>9391396.0</td>
      <td>13838616</td>
      <td>26824551.0</td>
      <td>14185941.0</td>
      <td>0.0</td>
      <td>16542725.0</td>
      <td>8381.0</td>
      <td>498856.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2018.0</td>
      <td>67556368178499</td>
      <td>17808057.0</td>
      <td>27291887</td>
      <td>51001756.0</td>
      <td>20300833.0</td>
      <td>0.0</td>
      <td>17193296.0</td>
      <td>0.0</td>
      <td>502637.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2019.0</td>
      <td>37667975559146</td>
      <td>10319129.0</td>
      <td>15539944</td>
      <td>29054786.0</td>
      <td>15411914.0</td>
      <td>0.0</td>
      <td>7084232.0</td>
      <td>0.0</td>
      <td>196541.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
cite2_2004to2014 = cite2yrs.loc[(cite2yrs['year'] >= 2004.0) & (cite2yrs['year'] <= 2014.0)]
cite2_2004to2014
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>Citation</th>
      <th>ExpYY</th>
      <th>ViolCode</th>
      <th>ViolFine</th>
      <th>Balance</th>
      <th>PenaltyDate</th>
      <th>OpenFine</th>
      <th>OpenPenalty</th>
      <th>CouncilDistrict</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>2004.0</td>
      <td>5929909208</td>
      <td>1142.0</td>
      <td>3860</td>
      <td>7985.0</td>
      <td>8240.0</td>
      <td>0.0</td>
      <td>3673.0</td>
      <td>2155.0</td>
      <td>58.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2005.0</td>
      <td>40143341317</td>
      <td>7438.0</td>
      <td>23573</td>
      <td>44565.0</td>
      <td>50852.0</td>
      <td>0.0</td>
      <td>40655.0</td>
      <td>4870.0</td>
      <td>510.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2006.0</td>
      <td>325847089541</td>
      <td>39841.0</td>
      <td>128173</td>
      <td>204672.0</td>
      <td>255737.0</td>
      <td>0.0</td>
      <td>196211.0</td>
      <td>3570.0</td>
      <td>2094.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2007.0</td>
      <td>3274128266047</td>
      <td>381597.0</td>
      <td>1138640</td>
      <td>1915819.0</td>
      <td>2252863.0</td>
      <td>0.0</td>
      <td>1903316.0</td>
      <td>23343.0</td>
      <td>40565.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2008.0</td>
      <td>2730980171881</td>
      <td>356333.0</td>
      <td>884699</td>
      <td>1579975.0</td>
      <td>1817096.0</td>
      <td>0.0</td>
      <td>1561574.0</td>
      <td>12030.0</td>
      <td>57745.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2009.0</td>
      <td>2936647980524</td>
      <td>404338.0</td>
      <td>889395</td>
      <td>1653234.0</td>
      <td>1842377.0</td>
      <td>0.0</td>
      <td>1608374.0</td>
      <td>228185.0</td>
      <td>58937.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2010.0</td>
      <td>3728444379924</td>
      <td>481453.0</td>
      <td>967703</td>
      <td>1973124.0</td>
      <td>2131881.0</td>
      <td>0.0</td>
      <td>1927679.0</td>
      <td>159457.0</td>
      <td>82724.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2011.0</td>
      <td>10805799688122</td>
      <td>1482399.0</td>
      <td>3676969</td>
      <td>6358346.0</td>
      <td>18331275.0</td>
      <td>0.0</td>
      <td>6272580.0</td>
      <td>13322533.0</td>
      <td>92867.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2012.0</td>
      <td>6763628192955</td>
      <td>1939530.0</td>
      <td>4609708</td>
      <td>7843721.0</td>
      <td>18421078.0</td>
      <td>0.0</td>
      <td>7001911.0</td>
      <td>12521072.0</td>
      <td>106336.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2013.0</td>
      <td>1718882502872</td>
      <td>720176.0</td>
      <td>1186059</td>
      <td>2889470.0</td>
      <td>12884423.0</td>
      <td>0.0</td>
      <td>2220923.0</td>
      <td>11615391.0</td>
      <td>89305.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2014.0</td>
      <td>4256522079363</td>
      <td>1148855.0</td>
      <td>1643654</td>
      <td>4210955.0</td>
      <td>12887230.0</td>
      <td>0.0</td>
      <td>2308770.0</td>
      <td>11035398.0</td>
      <td>133480.0</td>
    </tr>
  </tbody>
</table>
</div>



# Question II


```python
import math
import os
import random
import re
import sys
from collections import deque

class Point():
    def __init__(self, x, y, count):
        self.x = x
        self.y = y
        self.count = count


def checkBound(curP, a, b, n, check, myQ):
    X, Y = curP.x, curP.y

    if (X - a) >= 0:
        if (Y - b) >= 0 and check[X-a][Y-b] == 0:
            myQ.append(Point(X-a, Y-b, curP.count+1))
            check[X-a][Y-b] = 1
        if (Y + b) < n and check[X-a][Y+b] == 0:
            myQ.append(Point(X-a, Y+b, curP.count+1))
            check[X-a][Y+b] = 1
    if (X + a) < n:
        if (Y - b) >= 0 and check[X+a][Y-b] == 0:
            myQ.append(Point(X+a, Y-b, curP.count+1))
            check[X+a][Y-b] = 1
        if (Y + b) < n and check[X+a][Y+b] == 0:
            myQ.append(Point(X+a, Y+b, curP.count+1))
            check[X+a][Y+b] = 1
            if (X + a) == n-1 and (Y + b) == n-1:
                return curP.count + 1   ##Check for the target point
    return -1


def step(n, a, b):
    myQ = deque()
    check = [[0]*n for i in range(n)]  ##Check whether this point is visited or not

    start = Point(0, 0, 0)
    check[start.x][start.y] = 1
    myQ.append(start)

    while len(myQ) > 0:
        curP = myQ.popleft()
        count1 = checkBound(curP, a, b, n, check, myQ)
        count2 = checkBound(curP, b, a, n, check, myQ)
        if count1 > 0 or count2 > 0: 
            return max(count1, count2)

    return -1

print(step(1000,13,23))

def knightlOnAChessboard(n):
    res = [[0]*(n-1) for i in range(n-1)]
    for i in range(n-1):
        for j in range(i, n-1):
            res[i][j] = step(n, i+1, j+1)

    for i in range(1, n-1):
        for j in range(i):
            res[i][j] = res[j][i]

    return res

print(knightlOnAChessboard(5))
```

    67
    [[4, 4, 2, 8], [4, 2, 4, 4], [2, 4, -1, -1], [8, 4, -1, 1]]



```python

```


```python

```
