<template>
    <div>
        <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#addStaff">Thêm nhân viên</button>

        <div class="modal fade" id="addStaff" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-hidden="true">
            <div class="modal-dialog modal-xl">
                <div class="modal-content modal-add-staff">
                    <div class="modal-header">
                        <h5 class="modal-title">Thêm nhân viên</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <div class="text-center">
                            <label class="form-label">Ảnh đại diện</label>
                            <div class="avatar m-auto">
                                <img class="w-100" src="../assets/images/avatar.png" alt="avatar" />
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-lg-6 col-sm-12">
                                <div class="form">
                                    <label class="form-label mb-0">Họ và tên</label>
                                    <input type="text" class="form-control fs-14 mt-1" placeholder="Ví dụ: Nguyễn Văn A" v-model="formStaff.name" required />
                                </div>
                            </div>
                            <div class="col-lg-6 col-sm-12">
                                <div class="form">
                                    <label class="form-label mb-0">Tuổi</label>
                                    <input type="text" class="form-control fs-14 mt-1" placeholder="Nhập tuổi (18 - 35)" v-model="formStaff.age" />
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-lg-6 col-sm-12">
                                <div class="form">
                                    <label class="form-label mb-0">Số điện thoại</label>
                                    <input type="text" class="form-control fs-14 mt-1" placeholder="Nhập số điện thoại" v-model="formStaff.phone" />
                                </div>
                            </div>
                            <div class="col-lg-6 col-sm-12">
                                <div class="form">
                                    <label class="form-label mb-0">Email</label>
                                    <input type="text" class="form-control fs-14 mt-1" placeholder="Nhập email" v-model="formStaff.email" />
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-lg-6 col-sm-12">
                                <div class="form">
                                    <label class="form-label mb-0">Địa chỉ</label>
                                    <input type="text" class="form-control fs-14 mt-1" placeholder="Nhập địa chỉ" v-model="formStaff.address" />
                                </div>
                            </div>
                            <div class="col-lg-6 col-sm-12">
                                <div class="form">
                                    <label class="form-label mb-0">Thời gian tuyển</label>
                                    <input type="date" class="form-control fs-14 mt-1" v-model="formStaff.time" />
                                </div>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-lg-6 col-sm-12">
                                <div class="form">
                                    <label class="form-label mb-0">Bộ phận</label>
                                    <select class="form-select fs-14 mt-1" v-model="formStaff.lang">
                                        <option class="fs-14" :value="option" v-for="(option, index) in language" :key="index">{{ option }}</option>
                                    </select>
                                </div>
                            </div>
                            <div class="col-lg-6 col-sm-12"></div>
                        </div>
                        <div class="form">
                            <label class="form-label mb-0">Thông tin thêm</label>
                            <textarea class="form-control fs-14 mt-1" row="8" v-model="formStaff.moreInfo"></textarea>
                        </div>
                    </div>
                    <div class="modal-footer border-top-0">
                        <button type="button" class="btn btn-secondary" data-bs-toggle="modal" data-bs-target="#cancelAddStaff">Hủy</button>

                        <button type="button" class="btn btn-primary" data-bs-dismiss="modal" @click="addStaff">Thêm</button>
                    </div>
                </div>
            </div>
        </div>
        <div class="modal fade" id="cancelAddStaff" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content modal-sm m-auto">
                    <div class="modal-header border-bottom-0">
                        <h5 class="modal-title">Thông báo</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <p class="mb-0">Thêm mới nhân viên chưa được hoàn tất. Xác nhận hủy bỏ thao tác?</p>
                    </div>
                    <div class="modal-footer border-top-0">
                        <button type="button" class="btn btn-secondary btn-sm" data-bs-toggle="modal" data-bs-target="#addStaff">Quay lại</button>
                        <button type="button" class="btn btn-success btn-sm" data-bs-dismiss="modal" @click="cancelAdStaff">Đồng ý</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            newStaff: [],
            formStaff: [],
            language: ["Java", "Reactjs", "Angular", "Manual test", "Automation test", ".net"],
        };
    },
    methods: {
        addStaff() {
            if (this.formStaff.name && this.formStaff.age && this.formStaff.address && this.formStaff.email && this.formStaff.phone && this.formStaff.phone) {
                const id = this.newStaff.length;
                let formStaffCoppy = { id, ...this.formStaff };
                this.newStaff === this.newStaff.push(formStaffCoppy);
                this.formStaff = [];
                this.$emit("addNewStaff", formStaffCoppy);
            }
        },
        cancelAdStaff() {
            this.formStaff = [];
        },
    },
};
</script>
<style>
.form-label {
    font-weight: 500;
}

.form {
    margin-top: 12px;
}

.fs-14 {
    font-size: 14px !important;
}
</style>
