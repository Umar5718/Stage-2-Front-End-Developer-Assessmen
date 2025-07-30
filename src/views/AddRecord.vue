<template>
  <div class="flex h-screen bg-gray-50">
    <Sidebar :collapsed="isCollapsed" @toggle="toggleSidebar" />
    
    <div class="flex-1 flex flex-col overflow-hidden">
      <header class="bg-white shadow-sm border-b border-gray-200 px-6 py-4">
        <div class="flex items-center justify-between">
          <div class="flex items-center">
            <svg class="w-6 h-6 text-green-600 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
            </svg>
            <h1 class="text-xl font-semibold text-blue-600">Add Record</h1>
          </div>
          <div class="flex items-center space-x-2">
            <button class="p-2 text-blue-600 hover:bg-blue-50 rounded-lg">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
              </svg>
            </button>
            <button class="p-2 text-red-600 hover:bg-red-50 rounded-lg">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
        </div>
      </header>

      <main class="flex-1 overflow-y-auto p-8 bg-gray-50">
        <div class="max-w-4xl mx-auto">
          <div class="mb-8">
            <div class="flex items-center justify-center space-x-8">
              <div v-for="(step, index) in steps" :key="index" class="flex items-center">
                <div
                  class="w-10 h-10 rounded-full flex items-center justify-center text-sm font-medium transition-colors"
                  :class="currentStep === index + 1
                    ? 'bg-blue-600 text-white'
                    : currentStep > index + 1
                      ? 'bg-green-500 text-white'
                      : 'bg-gray-300 text-gray-600'">
                  <svg v-if="currentStep > index + 1" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                    <path fill-rule="evenodd"
                      d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                      clip-rule="evenodd" />
                  </svg>
                  <span v-else>{{ index + 1 }}</span>
                </div>
                <div v-if="index < steps.length - 1" class="w-16 h-1 mx-4 transition-colors"
                  :class="currentStep > index + 1 ? 'bg-green-500' : 'bg-gray-300'"></div>
              </div>
            </div>
          </div>

          <div class="bg-white rounded-lg shadow-sm border border-gray-200 p-8">
            <div v-if="currentStep === 1">
              <h2 class="text-xl font-semibold text-gray-800 mb-6 text-center">Create New Record</h2>
              <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Date received*</label>
                  <input 
                    type="text" 
                    placeholder="DD/MM/YYYY"
                    v-model="formData.step1.dateReceived"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Time received*</label>
                  <input 
                    type="text" 
                    placeholder="15:00:00"
                    v-model="formData.step1.timeReceived"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div></div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Customer title*</label>
                  <select
                    v-model="formData.step1.customerTitle"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    <option value="">Select title</option>
                    <option value="mr">Mr</option>
                    <option value="mrs">Mrs</option>
                    <option value="ms">Ms</option>
                    <option value="dr">Dr</option>
                  </select>
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Customer name</label>
                  <input 
                    type="text"
                    v-model="formData.step1.customerName"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">First name</label>
                  <input 
                    type="text"
                    v-model="formData.step1.firstName"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Date of birth</label>
                  <input 
                    type="date"
                    v-model="formData.step1.dateOfBirth"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Sex</label>
                  <select
                    v-model="formData.step1.sex"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    <option value="">Select sex</option>
                    <option value="male">Male</option>
                    <option value="female">Female</option>
                    <option value="other">Other</option>
                  </select>
                </div>
              </div>
            </div>

            <div v-if="currentStep === 2">
              <h2 class="text-xl font-semibold text-gray-800 mb-6 text-center">Judicial Case References</h2>
              <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Name OPJ</label>
                  <select
                    v-model="formData.step2.nameOPJ"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    <option value="">Select OPJ</option>
                    <option value="opj1">OPJ 1</option>
                    <option value="opj2">OPJ 2</option>
                  </select>
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Service Police</label>
                  <input 
                    type="text"
                    v-model="formData.step2.servicePolice"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">OPJ Grade</label>
                  <input 
                    type="text"
                    v-model="formData.step2.opjGrade"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">PV Number</label>
                  <input 
                    type="text"
                    v-model="formData.step2.pvNumber"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Nationality</label>
                  <select
                    v-model="formData.step2.nationality"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    <option value="">Select nationality</option>
                    <option value="french">French</option>
                    <option value="other">Other</option>
                  </select>
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">TGI of</label>
                  <select
                    v-model="formData.step2.tgiOf"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    <option value="">Select TGI</option>
                    <option value="paris">Paris</option>
                    <option value="lyon">Lyon</option>
                  </select>
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Magistrate Name</label>
                  <select
                    v-model="formData.step2.magistrateName"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    <option value="">Select magistrate</option>
                    <option value="mag1">Magistrate 1</option>
                    <option value="mag2">Magistrate 2</option>
                  </select>
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Magistrate Grade</label>
                  <select
                    v-model="formData.step2.magistrateGrade"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    <option value="">Select grade</option>
                    <option value="grade1">Grade 1</option>
                    <option value="grade2">Grade 2</option>
                  </select>
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Prosecutor's office number</label>
                  <input 
                    type="text"
                    v-model="formData.step2.prosecutorOfficeNumber"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Instruction number</label>
                  <input 
                    type="text"
                    v-model="formData.step2.instructionNumber"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
                <div>
                  <label class="block text-sm font-medium text-gray-700 mb-2">Justice identifier</label>
                  <input 
                    type="text"
                    v-model="formData.step2.justiceIdentifier"
                    class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                </div>
              </div>
            </div>

            <div v-if="currentStep === 3">
              <h2 class="text-xl font-semibold text-gray-800 mb-6 text-center">Seals</h2>
              
              <div class="mb-8">
                <h3 class="text-lg font-medium text-gray-800 mb-4">Seal 1</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                  <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Prosecution Date</label>
                    <input 
                      type="date"
                      v-model="formData.step3.prosecutionDate"
                      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Seal Date</label>
                    <select
                      v-model="formData.step3.sealDate"
                      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                      <option value="">Select date</option>
                      <option value="today">Today</option>
                      <option value="yesterday">Yesterday</option>
                    </select>
                  </div>
                </div>

                <div 
                  class="border-2 border-dashed rounded-lg p-8 text-center mb-6 transition-colors"
                  :class="isDragOver ? 'border-blue-400 bg-blue-50' : 'border-gray-300'"
                  @dragover.prevent="handleDragOver"
                  @dragleave.prevent="handleDragLeave"
                  @drop.prevent="handleDrop">
                  <input 
                    ref="fileInput"
                    type="file"
                    multiple
                    accept=".pdf,.jpg,.jpeg,.png,.doc,.docx"
                    @change="handleFileSelect"
                    class="hidden">
                  
                  <svg class="mx-auto h-12 w-12 text-gray-400 mb-4" stroke="currentColor" fill="none" viewBox="0 0 48 48">
                    <path
                      d="M28 8H12a4 4 0 00-4 4v20m32-12v8m0 0v8a4 4 0 01-4 4H12a4 4 0 01-4-4v-4m32-4l-3.172-3.172a4 4 0 00-5.656 0L28 28M8 32l9.172-9.172a4 4 0 015.656 0L28 28m0 0l4 4m4-24h8m-4-4v8m-12 4h.02"
                      stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                  </svg>
                  <p class="text-gray-600 mb-2">Drag files here to upload</p>
                  <button 
                    type="button"
                    @click="$refs.fileInput.click()"
                    class="bg-blue-600 text-white px-4 py-2 rounded-md hover:bg-blue-700 transition-colors">
                    Select Files
                  </button>
                  <p class="text-xs text-gray-500 mt-2">Supported formats: PDF, JPG, PNG, DOC, DOCX</p>
                </div>

                <div v-if="uploadedFiles.length > 0" class="space-y-2 mb-6">
                  <div 
                    v-for="(file, index) in uploadedFiles" 
                    :key="index"
                    class="flex items-center p-3 bg-gray-50 rounded-md">
                    <svg class="w-5 h-5 text-gray-400 mr-3" fill="currentColor" viewBox="0 0 20 20">
                      <path fill-rule="evenodd"
                        d="M4 4a2 2 0 012-2h4.586A2 2 0 0112 2.586L15.414 6A2 2 0 0116 7.414V16a2 2 0 01-2 2H6a2 2 0 01-2-2V4z"
                        clip-rule="evenodd" />
                    </svg>
                    <div class="flex-1">
                      <span class="text-sm text-gray-700">{{ file.name }}</span>
                      <span class="text-xs text-gray-500 ml-2">({{ formatFileSize(file.size) }})</span>
                    </div>
                    <button 
                      @click="removeFile(index)"
                      class="text-red-500 hover:text-red-700 ml-2">
                      <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd"
                          d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
                          clip-rule="evenodd" />
                      </svg>
                    </button>
                  </div>
                </div>
              </div>

              <div class="mb-8">
                <h3 class="text-lg font-medium text-gray-800 mb-4">Sample 1-A</h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                  <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Sample Date</label>
                    <input 
                      type="date"
                      v-model="formData.step3.sampleDate"
                      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Sample Type</label>
                    <select
                      v-model="formData.step3.sampleType"
                      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                      <option value="">Select type</option>
                      <option value="blood">Blood</option>
                      <option value="saliva">Saliva</option>
                      <option value="hair">Hair</option>
                    </select>
                  </div>
                  <div class="md:col-span-2">
                    <label class="block text-sm font-medium text-gray-700 mb-2">Sample Description</label>
                    <textarea 
                      rows="4"
                      v-model="formData.step3.sampleDescription"
                      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"></textarea>
                  </div>
                  <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">Preserved</label>
                    <select
                      v-model="formData.step3.preserved"
                      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                      <option value="">Select option</option>
                      <option value="yes">Yes</option>
                      <option value="no">No</option>
                    </select>
                  </div>
                </div>
              </div>

              <div class="text-center mb-6">
                <button 
                  type="button"
                  @click="addSample"
                  class="text-blue-600 hover:text-blue-800 font-medium">
                  + Add Sample
                </button>
              </div>
            </div>

            <div class="flex justify-between mt-8 pt-6 border-t border-gray-200">
              <button 
                v-if="currentStep > 1" 
                @click="previousStep"
                class="px-6 py-2 bg-green-500 text-white rounded-md hover:bg-green-600 transition-colors">
                Previous
              </button>
              <div v-else></div>
              
              <button 
                v-if="currentStep < steps.length" 
                @click="nextStep"
                class="px-6 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 transition-colors">
                Next
              </button>
              <button 
                v-else 
                @click="submitForm"
                class="px-6 py-2 bg-blue-600 text-white rounded-md hover:bg-blue-700 transition-colors">
                Submit
              </button>
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import Sidebar from '../components/Sidebar.vue';

export default {
  name: 'AddRecord',
  components: {
    Sidebar
  },
  data() {
    return {
      currentStep: 1,
      steps: ['Create New Record', 'Judicial Case References', 'Seals'],
      isDragOver: false,
      uploadedFiles: [],
      formData: {
        step1: {
          dateReceived: '',
          timeReceived: '',
          customerTitle: '',
          customerName: '',
          firstName: '',
          dateOfBirth: '',
          sex: ''
        },
        step2: {
          nameOPJ: '',
          servicePolice: '',
          opjGrade: '',
          pvNumber: '',
          nationality: '',
          tgiOf: '',
          magistrateName: '',
          magistrateGrade: '',
          prosecutorOfficeNumber: '',
          instructionNumber: '',
          justiceIdentifier: ''
        },
        step3: {
          prosecutionDate: '',
          sealDate: '',
          sampleDate: '',
          sampleType: '',
          sampleDescription: '',
          preserved: ''
        }
      }
    }
  },
  methods: {
    nextStep() {
      if (this.currentStep < this.steps.length) {
        this.currentStep++
      }
    },
    previousStep() {
      if (this.currentStep > 1) {
        this.currentStep--
      }
    },
    submitForm() {
      const formDataWithFiles = {
        ...this.formData,
        uploadedFiles: this.uploadedFiles
      }
      console.log('Form submitted:', formDataWithFiles)
      alert('Form submitted successfully!')
    },
    handleDragOver(e) {
      e.preventDefault()
      this.isDragOver = true
    },
    handleDragLeave(e) {
      e.preventDefault()
      this.isDragOver = false
    },
    handleDrop(e) {
      e.preventDefault()
      this.isDragOver = false
      const files = Array.from(e.dataTransfer.files)
      this.addFiles(files)
    },
    handleFileSelect(e) {
      const files = Array.from(e.target.files)
      this.addFiles(files)
      e.target.value = ''
    },
    addFiles(files) {
      const allowedTypes = [
        'application/pdf',
        'image/jpeg',
        'image/jpg',
        'image/png',
        'application/msword',
        'application/vnd.openxmlformats-officedocument.wordprocessingml.document'
      ]
      
      files.forEach(file => {
        if (allowedTypes.includes(file.type)) {
          const exists = this.uploadedFiles.some(existingFile => 
            existingFile.name === file.name && existingFile.size === file.size
          )
          
          if (!exists) {
            this.uploadedFiles.push(file)
          }
        } else {
          alert(`File type not supported: ${file.name}`)
        }
      })
    },
    removeFile(index) {
      this.uploadedFiles.splice(index, 1)
    },
    formatFileSize(bytes) {
      if (bytes === 0) return '0 Bytes'
      const k = 1024
      const sizes = ['Bytes', 'KB', 'MB', 'GB']
      const i = Math.floor(Math.log(bytes) / Math.log(k))
      return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i]
    },
    addSample() {
      console.log('Adding new sample...')
    },
    toggleSidebar() {
      this.isCollapsed = !this.isCollapsed
    }
  }
}
</script>