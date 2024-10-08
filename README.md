import React, { useState } from 'react';
import { Upload, FileSearch, AlertCircle, CheckCircle } from 'lucide-react';

const PlagiarismDetector = () => {
  const [file, setFile] = useState(null);
  const [result, setResult] = useState(null);
  const [loading, setLoading] = useState(false);

  const handleFileChange = (e) => {
    setFile(e.target.files[0]);
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    if (!file) return;

    setLoading(true);
    // Simulasi pengecekan plagiasi
    setTimeout(() => {
      setResult({
        similarityScore: Math.random(),
        details: "Hasil pengecekan plagiasi...",
      });
      setLoading(false);
    }, 2000);
  };

  return (
    <div className="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
      <div className="relative py-3 sm:max-w-xl sm:mx-auto">
        <div className="absolute inset-0 bg-gradient-to-r from-cyan-400 to-light-blue-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
        <div className="relative px-4 py-10 bg-white shadow-lg sm:rounded-3xl sm:p-20">
          <div className="max-w-md mx-auto">
            <div className="flex items-center space-x-5">
              <div className="h-14 w-14 bg-yellow-200 rounded-full flex items-center justify-center">
                <FileSearch size={28} className="text-yellow-500" />
              </div>
              <div className="block pl-2 font-semibold text-xl self-start text-gray-700">
                <h2 className="leading-relaxed">PlagiGuard</h2>
                <p className="text-sm text-gray-500 font-normal leading-relaxed">Deteksi Plagiasi Karya Ilmiah</p>
              </div>
            </div>
            <div className="divide-y divide-gray-200">
              <div className="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                <form onSubmit={handleSubmit} className="space-y-4">
                  <div className="flex items-center justify-center w-full">
                    <label className="flex flex-col rounded-lg border-4 border-dashed w-full h-60 p-10 group text-center">
                      <div className="h-full w-full text-center flex flex-col items-center justify-center">
                        <Upload className="w-10 h-10 text-blue-400 group-hover:text-blue-600" />
                        <p className="pointer-none text-gray-500 ">
                          <span className="text-blue-500 hover:underline">Pilih file</span> atau drag and drop
                        </p>
                      </div>
                      <input type="file" className="hidden" onChange={handleFileChange} />
                    </label>
                  </div>
                  <button type="submit" className="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                    {loading ? 'Memeriksa...' : 'Periksa Plagiasi'}
                  </button>
                </form>
              </div>
              {result && (
                <div className="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                  <div className="flex items-center space-x-2">
                    {result.similarityScore < 0.3 ? (
                      <CheckCircle className="text-green-500" />
                    ) : (
                      <AlertCircle className="text-red-500" />
                    )}
                    <p>Skor Kesamaan: {(result.similarityScore * 100).toFixed(2)}%</p>
                  </div>
                  <p>{result.details}</p>
                </div>
              )}
            </div>
          </div>
        </div>
      </div>
    </div>
  );
};

export default PlagiarismDetector;
