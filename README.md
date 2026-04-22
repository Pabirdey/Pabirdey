<!DOCTYPE html>
<html>
<head>
    <title>Raw Material Position</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" />

    <style>
        body {
            background-color: #f4f6f9;
        }

        .card-custom {
            background: linear-gradient(to right, #0d47a1, #1976d2);
            border-radius: 20px;
            padding: 20px;
            color: white;
        }

        .table-custom {
            background-color: white;
            border-radius: 10px;
            overflow: hidden;
        }

        .table-custom th {
            background-color: #1565c0;
            color: white;
            text-align: center;
            font-size: 14px;
        }

        .table-custom td {
            text-align: center;
            font-size: 13px;
            padding: 6px;
        }

        .table-custom td:hover {
            background-color: #e3f2fd;
            cursor: pointer;
        }

        .material-name {
            font-weight: bold;
            background-color: #e3f2fd;
        }

        .btn-custom {
            width: 120px;
            border-radius: 25px;
        }

        .table-container {
            max-height: 400px;
            overflow-y: auto;
        }
    </style>
</head>

<body>

<div class="container mt-4">

    <div class="card-custom">

        <h4 class="text-center mb-4">Raw Material Position</h4>

        <div class="table-container">
            <table class="table table-bordered table-custom">
                <thead>
                    <tr>
                        <th>Material</th>
                        <th>Yard</th>
                        <th>H.L</th>
                        <th>Stock</th>
                        <th>A</th>
                        <th>B</th>
                        <th>C</th>
                        <th>D</th>
                        <th>E</th>
                        <th>F</th>
                    </tr>
                </thead>

                <tbody>
                    <tr>
                        <td class="material-name">SINTER</td>
                        <td>R147</td><td>R148</td><td>R149</td>
                        <td>R150</td><td>R151</td><td>R152</td>
                        <td>R153</td><td>R154</td><td>R155</td>
                    </tr>

                    <tr>
                        <td class="material-name">TFO</td>
                        <td>R156</td><td>R157</td><td>R158</td>
                        <td>R159</td><td>R160</td><td>R161</td>
                        <td>R162</td><td>R163</td><td>R164</td>
                    </tr>

                    <tr>
                        <td class="material-name">LRP</td>
                        <td>R165</td><td>R166</td><td>R167</td>
                        <td>R168</td><td>R169</td><td>R170</td>
                        <td>R171</td><td>R172</td><td>R173</td>
                    </tr>

                    <tr>
                        <td class="material-name">JODA</td>
                        <td>R174</td><td>R175</td><td>R176</td>
                        <td>R177</td><td>R178</td><td>R179</td>
                        <td>R180</td><td>R181</td><td>R182</td>
                    </tr>

                    <tr>
                        <td class="material-name">PELLET</td>
                        <td>R383</td><td>R384</td><td>R385</td>
                        <td>R386</td><td>R387</td><td>R388</td>
                        <td>R389</td><td>R390</td><td>R391</td>
                    </tr>

                    <tr>
                        <td class="material-name">NUT COKE</td>
                        <td>R192</td><td>R193</td><td>R194</td>
                        <td>R195</td><td>R196</td><td>R197</td>
                        <td>R198</td><td>R199</td><td>R200</td>
                    </tr>

                    <tr>
                        <td class="material-name">LIMESTONE</td>
                        <td>R201</td><td>R202</td><td>R203</td>
                        <td>R204</td><td>R205</td><td>R206</td>
                        <td>R207</td><td>R208</td><td>R209</td>
                    </tr>

                    <tr>
                        <td class="material-name">SCRAP</td>
                        <td>R228</td><td>R229</td><td>R230</td>
                        <td>R231</td><td>R232</td><td>R233</td>
                        <td>R234</td><td>R235</td><td>R236</td>
                    </tr>
                </tbody>

            </table>
        </div>

    </div>

    <!-- Buttons -->
    <div class="text-center mt-4">
        <button class="btn btn-success btn-custom">Save</button>
        <button class="btn btn-danger btn-custom">Delete</button>
        <button class="btn btn-secondary btn-custom">Exit</button>
    </div>

</div>

</body>
</html>