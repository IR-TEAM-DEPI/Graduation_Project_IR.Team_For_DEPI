<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Project 7: Vulnerability Assessment and Remediation Plan</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Cairo', sans-serif;
            background-color: #0d1117;
            color: #c9d1d9;
        }
        .glass-card {
            background: rgba(22, 27, 34, 0.6);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(48, 54, 61, 0.5);
            transition: all 0.3s ease;
        }
        .glass-card:hover {
            border-color: rgba(139, 148, 158, 0.7);
            transform: translateY(-5px);
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.2);
        }
        .team-banner {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            padding: 12px 0;
            background: linear-gradient(90deg, rgba(31, 111, 235, 0.95), rgba(5, 150, 150, 0.95));
            color: white;
            text-align: center;
            z-index: 1000;
            animation: slideDownFadeIn 1s ease-out, fadeOut 1s ease-in 4s forwards;
            opacity: 0;
        }

        @keyframes slideDownFadeIn {
            from {
                transform: translateY(-100%);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        @keyframes fadeOut {
            from {
                opacity: 1;
            }
            to {
                opacity: 0;
                transform: translateY(-100%);
            }
        }
        .section-title {
            position: relative;
            padding-bottom: 10px;
            margin-bottom: 20px;
            font-weight: 900;
            font-size: 2.5rem;
            color: #58a6ff;
        }
        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            right: 0;
            width: 80px;
            height: 4px;
            background: #58a6ff;
            border-radius: 2px;
        }
        .timeline::before {
            content: '';
            position: absolute;
            top: 0;
            bottom: 0;
            right: 39px;
            width: 4px;
            background: #21262d;
            border-radius: 2px;
        }
        .timeline-item {
            position: relative;
            padding-right: 80px;
        }
        .timeline-item::before {
            content: attr(data-week);
            position: absolute;
            right: 0;
            top: 0;
            width: 80px;
            height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #161b22;
            border: 3px solid #30363d;
            color: #58a6ff;
            border-radius: 50%;
            font-weight: 700;
            font-size: 1.2rem;
            z-index: 1;
        }
        .deliverable-tag {
            background-color: rgba(56, 139, 253, 0.15);
            color: #58a6ff;
            border: 1px solid rgba(56, 139, 253, 0.4);
        }
    </style>
</head>
<body class="antialiased">

    <div id="team-banner" class="team-banner text-xl font-bold shadow-lg" style="display: none;">
        <p>🛡️ The Cyber Guardians Team 🛡️</p>
    </div>

    <div class="container mx-auto p-4 md:p-8">
        
        <!-- Header -->
        <header class="text-center my-12 pt-10">
            <h1 class="text-4xl md:text-6xl font-black text-white tracking-tight">
                <span class="bg-clip-text text-transparent bg-gradient-to-r from-blue-400 to-teal-300">
                    Project 7
                </span>
            </h1>
            <p class="mt-4 text-xl md:text-2xl font-bold text-gray-300">Vulnerability Assessment and Remediation Plan</p>
        </header>

        <!-- Objective Section -->
        <section class="my-16">
            <div class="glass-card rounded-xl p-8 max-w-4xl mx-auto text-center">
                <h2 class="text-2xl font-bold text-blue-400 mb-4">Objective</h2>
                <p class="text-lg text-gray-300 leading-relaxed">
                    Conduct a comprehensive vulnerability assessment on a system and develop a robust remediation plan to mitigate identified risks.
                </p>
            </div>
        </section>

        <!-- Project Timeline -->
        <section class="my-16">
            <h2 class="section-title text-center mb-12">Project Roadmap</h2>
            <div class="relative timeline max-w-5xl mx-auto">

                <!-- Week 1 -->
                <div class="timeline-item mb-12" data-week="Week 1">
                    <div class="glass-card rounded-xl p-6">
                        <h3 class="text-2xl font-bold text-teal-300 mb-3">Vulnerability Assessment Preparation</h3>
                        <div class="space-y-4">
                            <div>
                                <h4 class="font-bold text-lg text-white">Tasks:</h4>
                                <ul class="list-disc list-inside text-gray-400 mt-2 space-y-1">
                                    <li><strong class="text-gray-300">Select and Configure Assessment Tools:</strong> Choose tools like Nessus, OpenVAS, or Qualys and configure them.</li>
                                    <li><strong class="text-gray-300">Define Scope and Objectives:</strong> Identify systems, networks, or applications for assessment and set goals.</li>
                                </ul>
                            </div>
                            <div>
                                <h4 class="font-bold text-lg text-white">Deliverables:</h4>
                                <div class="flex flex-wrap gap-2 mt-2">
                                    <span class="deliverable-tag font-semibold py-1 px-3 rounded-full text-sm">Tool Configuration Documentation</span>
                                    <span class="deliverable-tag font-semibold py-1 px-3 rounded-full text-sm">Assessment Scope Document</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Week 2 -->
                <div class="timeline-item mb-12" data-week="Week 2">
                    <div class="glass-card rounded-xl p-6">
                        <h3 class="text-2xl font-bold text-teal-300 mb-3">Conduct Vulnerability Assessment</h3>
                        <div class="space-y-4">
                            <div>
                                <h4 class="font-bold text-lg text-white">Tasks:</h4>
                                <ul class="list-disc list-inside text-gray-400 mt-2 space-y-1">
                                    <li><strong class="text-gray-300">Perform Vulnerability Scanning:</strong> Run scans on the defined scope.</li>
                                    <li><strong class="text-gray-300">Analyze Scan Results:</strong> Review and categorize vulnerabilities by severity and impact.</li>
                                </ul>
                            </div>
                            <div>
                                <h4 class="font-bold text-lg text-white">Deliverables:</h4>
                                <div class="flex flex-wrap gap-2 mt-2">
                                    <span class="deliverable-tag font-semibold py-1 px-3 rounded-full text-sm">Vulnerability Scan Report</span>
                                    <span class="deliverable-tag font-semibold py-1 px-3 rounded-full text-sm">Initial Analysis Document</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Week 3 -->
                <div class="timeline-item mb-12" data-week="Week 3">
                    <div class="glass-card rounded-xl p-6">
                        <h3 class="text-2xl font-bold text-teal-300 mb-3">Develop Remediation Plan</h3>
                        <div class="space-y-4">
                            <div>
                                <h4 class="font-bold text-lg text-white">Tasks:</h4>
                                <ul class="list-disc list-inside text-gray-400 mt-2 space-y-1">
                                    <li><strong class="text-gray-300">Prioritize Vulnerabilities:</strong> Rank based on impact and ease of exploitation.</li>
                                    <li><strong class="text-gray-300">Create Remediation Strategies:</strong> Develop action items for fixing vulnerabilities.</li>
                                    <li><strong class="text-gray-300">Document Remediation Plan:</strong> Write a detailed plan with timelines and responsibilities.</li>
                                </ul>
                            </div>
                            <div>
                                <h4 class="font-bold text-lg text-white">Deliverables:</h4>
                                <div class="flex flex-wrap gap-2 mt-2">
                                    <span class="deliverable-tag font-semibold py-1 px-3 rounded-full text-sm">Prioritization Report</span>
                                    <span class="deliverable-tag font-semibold py-1 px-3 rounded-full text-sm">Remediation Plan</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Week 4 -->
                <div class="timeline-item" data-week="Week 4">
                    <div class="glass-card rounded-xl p-6">
                        <h3 class="text-2xl font-bold text-teal-300 mb-3">Implement and Verify Fixes</h3>
                        <div class="space-y-4">
                            <div>
                                <h4 class="font-bold text-lg text-white">Tasks:</h4>
                                <ul class="list-disc list-inside text-gray-400 mt-2 space-y-1">
                                    <li><strong class="text-gray-300">Apply Remediation Actions:</strong> Fix vulnerabilities as per the plan.</li>
                                    <li><strong class="text-gray-300">Verify Fixes and Conduct Follow-up Scans:</strong> Ensure vulnerabilities are resolved.</li>
                                    <li><strong class="text-gray-300">Prepare Final Report:</strong> Document the entire process and outcomes.</li>
                                </ul>
                            </div>
                            <div>
                                <h4 class="font-bold text-lg text-white">Deliverables:</h4>
                                <div class="flex flex-wrap gap-2 mt-2">
                                    <span class="deliverable-tag font-semibold py-1 px-3 rounded-full text-sm">Verification Report</span>
                                    <span class="deliverable-tag font-semibold py-1 px-3 rounded-full text-sm">Final Remediation Report</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- Team Section -->
        <section class="my-16">
            <h2 class="section-title text-center mb-12">Our Team</h2>
            <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-7 gap-6 max-w-6xl mx-auto">
                <div class="text-center">
                    <div class="p-2 bg-gray-800 rounded-full w-24 h-24 mx-auto flex items-center justify-center border-2 border-blue-400">
                        <span class="text-3xl font-bold text-white">AA</span>
                    </div>
                    <p class="mt-3 font-semibold text-gray-300">AbdulRhman AbdulGhaffar</p>
                </div>
                <div class="text-center">
                    <div class="p-2 bg-gray-800 rounded-full w-24 h-24 mx-auto flex items-center justify-center border-2 border-teal-300">
                        <span class="text-3xl font-bold text-white">YG</span>
                    </div>
                    <p class="mt-3 font-semibold text-gray-300">Yassa gerges</p>
                </div>
                <div class="text-center">
                    <div class="p-2 bg-gray-800 rounded-full w-24 h-24 mx-auto flex items-center justify-center border-2 border-blue-400">
                        <span class="text-3xl font-bold text-white">AL</span>
                    </div>
                    <p class="mt-3 font-semibold text-gray-300">Ahmed Leithy</p>
                </div>
                <div class="text-center">
                    <div class="p-2 bg-gray-800 rounded-full w-24 h-24 mx-auto flex items-center justify-center border-2 border-teal-300">
                        <span class="text-3xl font-bold text-white">YM</span>
                    </div>
                    <p class="mt-3 font-semibold text-gray-300">Yehia Mahmoud</p>
                </div>
                <div class="text-center">
                    <div class="p-2 bg-gray-800 rounded-full w-24 h-24 mx-auto flex items-center justify-center border-2 border-blue-400">
                        <span class="text-3xl font-bold text-white">GA</span>
                    </div>
                    <p class="mt-3 font-semibold text-gray-300">George Amir</p>
                </div>
                <div class="text-center">
                    <div class="p-2 bg-gray-800 rounded-full w-24 h-24 mx-auto flex items-center justify-center border-2 border-teal-300">
                        <span class="text-3xl font-bold text-white">FM</span>
                    </div>
                    <p class="mt-3 font-semibold text-gray-300">Fady Magdy</p>
                </div>
                <div class="text-center">
                    <div class="p-2 bg-gray-800 rounded-full w-24 h-24 mx-auto flex items-center justify-center border-2 border-blue-400">
                        <span class="text-3xl font-bold text-white">AM</span>
                    </div>
                    <p class="mt-3 font-semibold text-gray-300">Ali Mohamed</p>
                </div>
            </div>
        </section>

        <!-- Image Section -->
        <section class="my-16">
             <div class="max-w-5xl mx-auto glass-card rounded-xl p-4">
                <img src="http://googleusercontent.com/file_content/0" alt="Digital Egypt Pioneers Initiative" class="rounded-lg w-full h-auto shadow-2xl">
            </div>
        </section>

    </div>

    <script>
        // JavaScript to control the banner animation
        document.addEventListener('DOMContentLoaded', (event) => {
            const banner = document.getElementById('team-banner');
            
            function showBanner() {
                banner.style.display = 'block';
                // Reset animation
                banner.style.animation = 'none';
                banner.offsetHeight; /* trigger reflow */
                banner.style.animation = 'slideDownFadeIn 1s ease-out, fadeOut 1s ease-in 4s forwards';
            }

            // Show the banner initially
            showBanner();
            
            // And then show it every 10 seconds
            setInterval(showBanner, 10000); 
        });
    </script>
</body>
</html>
