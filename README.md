# World_Bank_Dataset

Código del editor avanzado:

let
  Origen = Csv.Document(File.Contents("E:\Descargas\world_bank_dataset.csv"), [Delimiter = ",", Columns = 8, QuoteStyle = QuoteStyle.None]),
  #"Encabezados promovidos" = Table.PromoteHeaders(Origen, [PromoteAllScalars = true]),
  #"Tipo de columna cambiado" = Table.TransformColumnTypes(#"Encabezados promovidos", {{"Country", type text}, {"Year", Int64.Type}, {"GDP (USD)", Int64.Type}, {"Population", Int64.Type}, {"Life Expectancy", Int64.Type}, {"Unemployment Rate (%)", Int64.Type}, {"CO2 Emissions (metric tons per capita)", Int64.Type}, {"Access to Electricity (%)", Int64.Type}}, "es"),
  // Modifiqué el nombre de la columna GDP a Gross Domestic Product porque tenía un nombre técnico y no resultaba de fácil lectura para quienes no conocieran las siglas.
  MiTransformacionManual = Table.RenameColumns(#"Tipo de columna cambiado", {{"GDP (USD)", "Gross Domestic Product (USD)"}}),
  Personalizado = #"MiTransformacionManual"
in
  Personalizado

Respuestas:
1) ¿Por qué es útil para un analista de datos entender la estructura let … in?
Porque es la forma en la que el lenguaje M organiza las instrucciones. Conocer y entender la estructura let...in permite al analista:
- renombrar pasos para mayor claridad: al hacer cambios o ajustes, en un equipo de trabajo permite que sea mucho más fácil auditar por otros compañeros.
- optimización de consultas: en muchos casos los analistas editan el código M para asegurar que el servidor SQL haga el trabajo pesado antes de que los datos lleguen a Power BI y éste no se vuelva lento.
- transformaciones que no tienen botón: existen funciones que a veces requieren ajustes manuales en el Editor Avanzado para funcionar con precisión.

2) ¿Qué significa que el lenguaje M sea Case Sensitive y cuál es la consecuencia práctica de ignorarlo?
El lenguaje M es Case Sensitive porque detecta diferencias entre funciones con mayúsculas y minúsculas, además de que las funciones nativas del lenguaje M siempre empiezan con mayúscula. Si se ignora esta práctica, la función puede ser interpretada de manera errónea o arrojar errores.

3) ¿Por qué elegiste ese dataset y qué criterios usaste para seleccionarlo?
Me pareció un dataset robusto, con información que puede ser útil para su análisis y al tener mucha información técnica tiene trabajo para realizar como renombrar columnas, borrar datos nulos y ordenar su contenido.
