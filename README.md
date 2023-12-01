Предполагается, что у вас есть фрейм данных с именем df

Сначала вы можете составить список возможных числовых типов, а затем просто выполнить цикл

numerics = ['int16', 'int32', 'int64', 'float16', 'float32', 'float64']
for c in [c for c in df.columns if df[c].dtype in numerics]:
    df[c] = np.log10(df[c])
Или однострочное решение с лямбда-оператором и np.dtype.kind

numeric_df = df.apply(lambda x: np.log10(x) if np.issubdtype(x.dtype, np.number) else x)

Если большинство столбцов являются числовыми, возможно, имеет смысл просто try это сделать и пропустить столбец, если это не работает:

for column in df.columns:
    try:
        df[column] = np.log10(df[column])
    except (ValueError, AttributeError):
        pass
Конечно, если вы хотите, вы могли бы обернуть это в функцию.

Если все столбцы числовые, вы даже можете просто выполнить

df_log10 = np.log10(df)



Вы можете использовать select_dtypes и numpy.log10:

import numpy as np
for c in df.select_dtype(include = [np.number]).columns:
    df[c] = np.log10(df[c])


использовать просто 
 numeric_df = df.apply(lambda x: np.log10(x)), без необходимости проверять тип столбца
